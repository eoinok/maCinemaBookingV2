# Week 5 Lab - A React Native Cinema Booking Application
This lab aims to build on previous techniques by using local persistent storage within our app to store data.

Goal
The goals for this weeks lab are
- To build on the previous cinema booking example
- To add a single json object to store booking details in a hook
- To pass the state and the setState using props to the PersonalInfo Component and the MovieBooking Component
- To use a UUID unique identifier generated from the Crypto library
- To store the booking as a json object using local data AsyncStorage.setItem()
- To retrieve the data from local storage using AysncStorage.getItem()

# Part 1
Add the following code snippet inside the App.js component. Place it inside the App() function but before the return () block.
```
const [booking, setBooking] = useState({
      bookDate: "2000-02-02",
      movieTitle: "",
      numberOfSeats: 0,
      balcony: 0,
  });
```
This code sets up the booking as a single json object with a number of different attributes. These values are initialised to 0 or "" or a test date. In order to pass this data into the PersonalInfo component and the MovieBooking component we will introduce two props data and setData to each component. To pass this data via props add
```
data={booking} setData={setBooking}
```
as props when loading the ```<PersonalInfo/>``` and ```<MovieBooking/>``` components
To allow this data to be received by those components change the function headers in each of the files for PersonalInfo and MovieBookings inside the components folders.
Inside the function headers for both components three arguments should now be received in the following form
```export default function PersonalInfo({screenstyle, data, setData})```
This should be similar in the MovieBooking header. 
Introduce the following functions into the MovieBooking component. Place it below the function header but before the return block
```
 function handleChangeMovieTitle(newTitle) {
    setData(data => ({
      ...data, // spread the previous booking properties
      movieTitle: newTitle // update only the movieTitle
    }));
  };
```
To get this function to work when movie changes, we need to chnage the onChange event in the props of the relevant components. To do this add the following snippet of code inside the ```<Picker.....>``` component.
```
onValueChange={(itemValue) => handleChangeMovieTitle(itemValue)}>
```
Now when the user selects a different movie from the Dropdown, the data inisde the booking object will change at the App.js level.

# Part 2
Add the line 
```import * as Crypto from 'expo-crypto';```
At the top of App.js to import the Crypto package from expo-crypto
Add the following line of code just inside the App() function - as the first line of code in that function.
```var uuid = Crypto.randomUUID();//this uses the Crypto library to generate a Universal Unique Identifier```

Add a new function in App.js called saveData - it should take no arguments. This function should be inside the App() function but before the return statement
Add the following line of code at the bottom of your screen i.e. place it below the swiper component
``` <TouchableOpacity style={styles.button} onPress={saveData}><Text style={{fontSize: 24, fontWeight: "bold"}}>Save Data</Text></TouchableOpacity>```
This line uses a TouchableOpacity which can make any element behave like a button. It's a little bit more sophisticated than a button and has some additional features but in this case we will use it like a button.
When this button is clicked, the onPress event will look to call a function called saveData(). Until we give it that function we will get an error so add the following function inside the App() function but before the render().
```
  async function saveData(){
    //alert("UUID="+uuid);//use this if on web
    Alert.alert("UUID="+uuid);//use this if on phone or virtual device
  }
```
Try this - click on the Save Data button, if it works, it should output a really long string of random letters and numbers - i.e. a Universal Unique Identifier.

# Part 3


# Part 3
Add a Toggle Switch to the MovieBooking Component. To do this:
- Add a new useState hook to the top of the file with the other useState hooks. Call this [balcony, setBalcony]
- Add a Switch component to the list of components being imported from react-native at the top of the Screen
- Pass the following props to the Switch component - ***value={balcony} onValueChange={setBalcony}*** this first ties the value of the Switch to whatever is stored in the balcony useState hook. The second make sure that whenever the toggle switch changes that the new value (true or false) is passed to the balcony state using the setBalcony hook function.
When you get this working, commit and push your changes.

# Part 4 
Replace the hardcoded items in the dropdown picker list with values from a Json array. To do this add the following snippet of code inside the MovieBooking function but before the return statement - after the other useState hooks. 
```
const [movieList, setMovieList] = useState([
   {'id': 1, "title": "Kneecap", "age": 16},
   {'id' : 2, "title": "Joker, Folie a Deux", "age": 18}, 
   {'id': 3, "title": "Deadpool and Wolverine", "age": 12}
  ]);
```
This code sets up an array of movies, each one with it's own unique key and some information about each movie. Currently the dropdown ```<Picker></Picker>``` component has two hard coded movies in the list inside ```<Picker.Item></Picker.Item>``` tags. We need to ***replace*** these with a function which will loop through each item in our movieList array and add a new ```<Picker.Item>``` for each element in the array. The following snippet of code will loop through each element in the array.
```
{ movieList.map((movie) => {
          return //add code here which will produce an appropriate <Picker.Item> tag for each movie. instead of hard coding the label and value use {movie.title}
          })}
```
