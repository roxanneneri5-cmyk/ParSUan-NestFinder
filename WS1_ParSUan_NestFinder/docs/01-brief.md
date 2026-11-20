# Project Brief: ParSUan NestFinder

## 1. The problem
Who has the problem, and what is hard for them today? (2–3 sentences)

## Students of Partido State University – Goa Campus often have difficulty finding reliable boarding houses, dormitories, and apartments near the campus. Property information is scattered across social media and word of mouth, making it difficult to compare rental prices, room availability, inclusions, house rules, and locations. Property owners also need an organized way to manage their listings, available rooms, and student inquiries.

## 2. Users and what they need to do
| User role | What they need to do in the app |
|-----------|---------------------------------|
| e.g. Student | Report a lost item, search found items |
| e.g. Admin   | Approve claims, manage categories   |


| User role | What they need to do in the app |
|-----------|---------------------------------|
| Student   | Search and filter accommodations, view property   details       and locations, save favorites, send inquiries, report incorrect information, and submit verified reviews. |
| Owner     | Register, manage property listings and rooms, update prices and available slots, respond to inquiries, confirm stays, and reply to reviews. |
| Admin      | Verify owners and property listings, manage user accounts, review reports, moderate reviews, and monitor system information. |
## 3. The database behind it
Database name, number of tables, and one sentence per table.

## Database name: ParSUan NestFinder

| Database component | Description |
|--------------------|-------------|
| Database Name | parsuan_nestfinder |
| Number of Tables | 16 |
| users | Stores user accounts, login information, roles, and account status. |
| students | Stores student profile information, including student number, course, year level, hometown, and gender. |
| owners | Stores owner profiles, verification status, and identification document paths. |
| campuses | Stores campus names, addresses, and geographic coordinates. |
| properties | Stores boarding house, dormitory, and apartment listings, including addresses, locations, rules, and descriptions. |
| rooms | Stores room types, rental prices, total slots, and available slots. |
| inclusions | Stores services and amenities included in the rental price, such as water and Wi-Fi. |
| room_inclusions | Connects rooms with their included amenities. |
| property_photos | Stores photo paths associated with each property. |
| favorites | Records properties saved by students. |
| inquiries | Records student inquiries or reservation requests about specific rooms and their statuses. |
| stays | Records student stays, including dates and owner confirmation. |
| reports | Stores student reports about incorrect property information or map locations. |
| reviews | Stores verified student reviews of confirmed stays, including cleanliness and safety ratings. |
| review_replies | Stores owner replies to student reviews. |
| notifications | Stores notification messages sent to system users and their read status. |

## 4. Must-have features (for the final project)
List 4–6. Each one should start with a verb: "Add...", "Search...", "Approve..."

- Search and filter boarding houses, dormitories, and apartments using property details, room types, prices, and availability.

- Display property details, photos, inclusions, house rules, map locations, and estimated distance to Partido State University – Goa Campus.

- Provide a Get Directions link that opens Google Maps with written landmark directions.

-Allow students to save favorite properties, send room inquiries, and report incorrect property information or locations.

- Enable owners to manage property listings, room information, rental prices, available slots, inquiries, and confirmed stays.

- Allow administrators to verify owners and listings, moderate reports and reviews, and manage user accounts.

## 5. Nice-to-have features (only if there's time)
List 1–3.

- Improve the property search experience with additional filtering and sorting options.

- Improve the presentation of property locations and estimated distances.

- Enhance the notification interface for students and property owners.

## 6. Similar apps I looked at
Name 1–2 real websites or apps and one idea you'll borrow from each.

- Airbnb – A reference for property listing layouts, accommodation details, photos, and search filters.

- Rentpad – A reference for displaying rental properties, prices, and available accommodations.