# Week 5 Lab - A React Native Cinema Booking Application
Goals
The goals for this weeks lab are
- To build on React Native UI Components knowlege
- To use a Swiper to access different screens
- To use a Dropdown "Picker" to select different items
- To use a DateTimePicker to access the calendar function of the device
- To use the Javascript array map function to populate a picker with data from a json array

# Part 1
This app includes the ability to add additional screens using a Swiper. So far just one screen for the Cinema booking (PersonalInfo) has been included. To include a second screen MovieBooking we need to do two things
- Import the MovieBooking component from the file ./components/MovieBooking.js
- Add the component inside the ```<Swiper></Swiper>``` Component - alongside the PersonalInfo component.
Do both of these in an identical fashion to the way in which the PersonalInfo component has been added. I.e. pass screenstyle={styles.screen} as a prop.
When you get this working, commit and push your changes.

# Part 2
Change the image at the top of the screen to something else associated with Movies. To do this, download a file (jpg or png) from the web. Save it to the assets folder and then change the reference to the file within App.js inside the IMG tag.
When you get this working, commit and push your changes.

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
