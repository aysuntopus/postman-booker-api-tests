# restful-booker-api-tests
App links :  [Restful -Booker](https://restful-booker.herokuapp.com/),  [Restful-Booker API Docs](https://restful-booker.herokuapp.com/apidoc/index.html)

_Restful-Booker_  is a simple Node booking form for testing RESTful web services created by Mark Winteringham. It features authentication and CRUD operations, includes a bunch of bugs for testers to explore.

# Run

In order to use this repository, you need to clone the project using this command line:

```bash
git clone https://github.com/aysuntopus/postman-booker-api-tests
```
You can open and examine test scripts inside the src components via the postman.

Newman is needed to run the test directly. If newman is not installed, install newman packages via npm with the following command.
```bash
npm install -g newman
```
For detailed installation, you can visit [here](https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman/).

You can start the testing process by running the run-newman file from the terminal.

You can also run this command manually as follows.
```bash
newman run “src/Booker API Test.postman_collection.json” -d BookerTestData.csv
```
# Issues Found
As mentioned in advance, _Restful-Booker_ contains some bugs for us :)
I would like to share the bugs I found:

`https://restful-booker.herokuapp.com/booking` - CreateBooking
-  A new booking can be added with a check-in date before the current date: Booking can be made for past dates.
- A new booking can be added with a check-in date after the check-out date: Booking can be created with a check-in date after the check-out date.
-  A new booking can be added with negative or zero totalprice: Creating booking with zero/negative total prices should be prevented.
- A new booking can be added without name: Creating booking without name should be prevented.
`https://restful-booker.herokuapp.com/booking` - Booking GetBookingIds
- Filter with check-in date doesn't work with after current date: Filtering check-in date with past date works but does not work when using a date later than the current date.
- Filter with both check-in & check-out date doesn't work: Filtering chek-in & check-out date it doesn't show existing booking.
`https://restful-booker.herokuapp.com/booking/:id` - UpdateBooking
-  Update with invalid value returns 200 : When updating the reservation with float totalprice, it returns with status code 200 even though the reservation record is unchanged.
-  Update with negative totalprice value returns 200 : When updating the reservation with negative total price, it returns with status code 200 and record is changed with new value.
`https://restful-booker.herokuapp.com/booking/1`  - Delete Booking
-   Auth can be set only via Cookie header, doesn't work with Authorization header.
-   Delete request returns 201 Created: It would be more accurate to use 200.
-   Delete  booking with invalid id returns 405: even though the query type is correct. It would be more correct to use 404 instead.