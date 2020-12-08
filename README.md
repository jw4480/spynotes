Courses
Back to Course
Final Project - Spy Notes
For your final project, you will be creating a privacy-focused note taking web application. The application will most likely be composed of a few separate pages but as long as all of the requirements listed below are met, you are free to approach this problem how you like.

Part 1: Registration
Your app should have a page (or a widget somewhere) that allows a user to sign up for an account. Rather than doing form validation again, this application will use a different sign up mechanism. Because we are building a privacy-focused note-taking app, your site should not collect any information from its users. Instead, the user simply clicks a button and we make an account for them. A server (at https://spy-notes-api.rk0.xyz) will generate a unique user code and a QR code to go along with it. When the user signs in in the future, they can either present their QR code or enter the text code on the sign up page. This is not necessarily super secure but it's kinda fun

Your job is to create a registration page with a single button. When the user clicks the button, your page should make a POST request to https://spy-notes-api.rk0.xyz/users (no parameters). If this request succeeds, the server will send back a new user code. Your page should display this code as text. Additionally, the code can be used to create an image URL that will be your QR code. If the user ID is abc-123, you would create an image like <img src="https://spy-notes-api.rk0.xyz/users/abc-123/qr"> somewhere on the page.

Part 2: Sign In
Your secure note-taking app should have a sign-in page. This is the page where the user can either enter their unique user ID from before or present their QR Code (via webcam). To enter their user ID, they should just be able to copy-paste it into a textbox. Presenting the QR Code will be a bit more interesting (but not too hard!). To read a QR code, you should use a JavaScript library. Don't try to do it by hand. In my sample lab, I used https://github.com/cozmo/jsQR. There may be an easier QR code reader library out there but I haven't experimented too much. The QR code library should help you extract a a User ID string from the QR Code. This is the same code that the user would be entering manually if they opted for that approach (if the text version is abc-123, the QR Code library should also extract abc-123).

You can use this code to redirect the user to the final page of your app, where the user will actually enter their notes. Once you have the user code, you should use it to redirect the user to a URL like /notes?userId=abc-123.

Part 3: Taking Notes
The final part of your app should be a place for the user to take notes. When the user loads the page, you should make a GET request to https://spy-notes-api.rk0.xyz/users/abc-123/notes. This will load any notes the user had previously saved on the server. If the user had saved notes, you should display these notes in a list. Notes should have a title and content property but will also have a noteId field with a unique ID.

There should also be a text input for the user to take more notes. If the user saves a note, you should make a POST request to https://spy-notes-api.rk0.xyz/users/abc-123/notes. The body of your POST request should be a JSON string that contains a title property and a content property. Making this request saves the user's note so that next time you run the GET request above, you will see their new note.

Finally, users should have an option to delete their notes (you can decide how that looks). If the user decides to delete a note, you will need to make a DELETE request to https://spy-notes-api.rk0.xyz/notes/def-456 (where def-456 is the note's unique ID).

Other Requirements
Your site should be responsive
You should have clean HTML and CSS code with no syntax errors
Hints
Don't try to do this all at the last minute
The QR code reader portion may seem daunting but it actually ends up being ~10 lines of code with the help of a library. You don't necessarily need to understand everything in the example to make it work.
You'll need to use Live Server (or some other server) for this assignment. Loading files directly in the browser will not let you make some of the server calls you need for this assignment. Please let me know if you have issues making this work.
Sample Site
I wrote a little sample site for this project so that you can see the general flow. It's a rough draft at the moment so some things might break. Also, it is not currently responsive. I plan to polish it up a bit in the next few days. You do not need to make your site look exactly like mine or behave exactly like mine. You can probably simplify the design quite a bit and still meet the requirements above.

Sample Site: https://spy-notes.rk0.xyz