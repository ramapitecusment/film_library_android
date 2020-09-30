# Film Library Application Android

According to research, users spend much more time in mobile apps than on mobile versions of 
websites. They also perform more unique actions in them. This is directly related to the 
ease of development: close integration with the smartphone operating system makes the app 
interface intuitive. A person knows what result this or that action will lead to, because 
they have seen a similar implementation in other applications.

By creating the film library app, you can significantly increase your profit, for example, 
from subscriptions or advertising banners.

**Requirements:**
1. Implement dynamic loading of movies;
2. Implement the ability to add movies to "Liked»;
3. implement content sorting by popularity, year, and other parameters;
4. To provide the greatest support devices on the platform Android;

**User requirements:**
1. Scroll through the list of movies;
2. By clicking on the movie poster you will receive more information on the film;
a. the name is in Russian and original
b. premiere date
c. Rating
d. Description
e. Trailers
f. Reviews
3. Watch trailers by redirecting to YouTube;
4. Add your movies to "Favorite".

**Dependencies:**
```
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'androidx.appcompat:appcompat:1.2.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.0.1'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'androidx.test.ext:junit:1.1.2'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.3.0'
    implementation 'androidx.recyclerview:recyclerview:1.1.0'
    implementation 'com.squareup.picasso:picasso:2.71828'

    def lifecycle_version = "1.1.1"

    // ViewModel and LiveData
    implementation 'androidx.lifecycle:lifecycle-extensions:2.2.0'

    annotationProcessor 'androidx.lifecycle:lifecycle-compiler:2.2.0'

    // optional - ReactiveStreams support for LiveData
    implementation 'androidx.lifecycle:lifecycle-reactivestreams:2.2.0'

    // optional - Test helpers for LiveData
    testImplementation 'androidx.arch.core:core-testing:2.1.0'

    def room_version = "1.1.1"

    implementation 'androidx.room:room-runtime:2.2.5'
    annotationProcessor 'androidx.room:room-compiler:2.2.5'

    // optional - RxJava support for Room
    implementation 'androidx.room:room-rxjava2:2.2.5'

    // optional - Guava support for Room, including Optional and ListenableFuture
    implementation 'androidx.room:room-guava:2.2.5'

    // Test helpers
    testImplementation 'androidx.room:room-testing:2.2.5'
    implementation 'androidx.cardview:cardview:1.0.0'
}
```

3 Activities:
1. MainActivity;
2. Detail Activity - displays detailed information about the movie: Title, 
original title, premiere date, description, poster, reviews, trailers;
3. Favourite Activity - displays a list of your Favorite movies.

Working with the database:
1. MainViewModel;
2. Movie - Stores all variables that store General information about the 
movie (Title, original title, premiere date, description, poster, reviews, 
trailers). Constructor as well as getter and setter in order to provide the 
greatest protection of data from changes during operation;
3. MovieDao;
4. MovieDatabase;
5. FavouriteMovie;
6. Review;
7. Trailer.

Working with JSON:
1. NetworkUtils - Getting data from the Internet in JSON format;
2. JSONUtils - convert data from JSON to an object.

These variables store keys-values that we get from the website by type: 
key:value. Using the key, we can select the values we need about the movie 
(Title, original title, premiere date, description, poster, reviews, trailers).

Data will be collected from https://www.themoviedb.org. You need to generate the API key.

The build URL method creates a link by adding the variables and creates from the link 
https://api.themoviedb.org/3/discover/movie links that change depending on the user's 
request, for example:

```
https://api.themoviedb.org/3/discover/movie?api_key=ee55b7f36b111de49bfcec75a51f706a&language=ru-RU&sort_by=popularity.desc&include_adult=false&include_video=false&page=1
```

The Movieduo interface is a database built into Java. This interface stores queries 
to the database of movies, movies you like, and can delete and add movies to the screen 
and to the list of movies you like.

The Movie Database class is abstract. It extends the Room Database class. Creating the 
getInstance method. This method checks whether the database exists, and if not, it 
will be created.

The MainViewModel class creates queries to the database of movies (getAllMovies), 
liked movies (getAllFavouriteMovies), can delete (deleteMovie) and add (insertMovie) 
movies to the screen, and creates a list of liked movies (deleteFavouriteMovie and 
insertFavouriteMovie).

The ReviewAdapter class creates a window for displaying reviews (onCreateViewHolder) on the 
DetailActivity activity. This window is filled in using the mandatory onBindViewHolder 
method. The getItemCount method stores the number of movie reviews. The set Reviews method 
displays movie reviews.

![alt text](https://raw.githubusercontent.com/ramapitecusment/film_library_android/master/images/1.jpg)
![alt text](https://raw.githubusercontent.com/ramapitecusment/film_library_android/master/images/2.jpg)
![alt text](https://raw.githubusercontent.com/ramapitecusment/film_library_android/master/images/3.jpg)
![alt text](https://raw.githubusercontent.com/ramapitecusment/film_library_android/master/images/4.jpg)
![alt text](https://raw.githubusercontent.com/ramapitecusment/film_library_android/master/images/5.jpg)