### **Data Model: AMC Premiere Finder**

This document describes the data structures required for the application. The model is designed to be database-agnostic but represents a logical separation of data into different objects or tables.

### 1\. User

Stores information about the app user, primarily for personalization and notifications.

| Attribute Name | Data Type | Description |
| :--- | :--- | :--- |
| `user_id` | `UUID` | **Primary Key.** A unique identifier for the user. |
| `device_token` | `String` | The unique token for the user's device, used for sending push notifications. |
| `manual_location_zip` | `String` | Stores the ZIP code if the user enters their location manually. |
| `notifications_enabled` | `Boolean` | `true` if the user has opted-in to receive push notifications. |
| `watchlist_movie_ids` | `Array<UUID>` | An array of `movie_id`s that the user has saved. (For future use). |
| `created_at` | `DateTime` | Timestamp when the user profile was created. |
| `updated_at` | `DateTime` | Timestamp of the last profile update. |

\<br\>

### 2\. Movie

Contains all details related to a specific film. This data would likely be sourced from a third-party movie database API and augmented with AMC-specific info.

| Attribute Name | Data Type | Description |
| :--- | :--- | :--- |
| `movie_id` | `UUID` | **Primary Key.** Unique identifier for the movie. |
| `title` | `String` | The official title of the movie (e.g., "Dune: Part Two"). |
| `synopsis` | `Text` | A paragraph summarizing the movie's plot. |
| `poster_url` | `String` | A URL pointing to the movie's poster image. |
| `trailer_url` | `String` | A URL to the movie's official trailer (e.g., a YouTube link). |
| `mpaa_rating` | `String` | The MPAA rating (e.g., "G", "PG", "PG-13", "R"). |
| `runtime_minutes` | `Integer` | The length of the movie in minutes. |
| `release_date_utc` | `Date` | The official U.S. release date for the movie. Used to determine premiere window. |
| `genres` | `Array<String>` | A list of genres associated with the movie (e.g., `["Action", "Sci-Fi"]`). |
| `cast` | `Array<String>` | A list of the main cast members. |
| `updated_at` | `DateTime` | Timestamp when the movie's data was last refreshed. |

\<br\>

### 3\. Theater

Represents a physical AMC Theatre location.

| Attribute Name | Data Type | Description |
| :--- | :--- | :--- |
| `theater_id` | `UUID` | **Primary Key.** Unique identifier for the AMC theater. |
| `name` | `String` | The name of the theater (e.g., "AMC Metreon 16"). |
| `address` | `String` | The full street address of the theater. |
| `latitude` | `Float` | The geographic latitude for mapping and distance calculation. |
| `longitude` | `Float` | The geographic longitude for mapping and distance calculation. |
| `updated_at` | `DateTime` | Timestamp when the theater's data was last refreshed. |

\<br\>

### 4\. Showing

This is the central "join" table that connects a movie to a theater at a specific time. It is the core of the app's functionality.

| Attribute Name | Data Type | Description |
| :--- | :--- | :--- |
| `showing_id` | `UUID` | **Primary Key.** A unique identifier for this specific showtime. |
| `movie_id` | `UUID` | *Foreign Key.* Connects to the `Movie` being shown. |
| `theater_id` | `UUID` | *Foreign Key.* Connects to the `Theater` where it's playing. |
| `showtime_utc` | `DateTime` | The exact date and time of the showing in UTC. |
| `format` | `String` | The format of the showing (e.g., "Standard", "Dolby Cinema", "IMAX"). |
| `ticketing_url` | `String` | The deep link URL to the ticket purchasing page on the AMC website/app. |
| `is_premiere` | `Boolean` | **Crucial Flag.** `true` if this showing falls within the defined premiere window (e.g., Thurs-Fri of release week). This flag powers the entire app. |
| `is_sold_out`| `Boolean` | `true` if the showtime is sold out. Fetched in real-time or near real-time. |
| `updated_at` | `DateTime` | Timestamp when this showtime's status was last checked. |

\<br\>

### Relationships

  * A `Movie` can have many `Showing`s.
  * A `Theater` can have many `Showing`s.
  * A `Showing` belongs to exactly one `Movie` and one `Theater`.
  * A `User` can have a `watchlist` that contains many `Movie`s (a many-to-many relationship).
