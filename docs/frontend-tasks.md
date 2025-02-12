# Frontend Task Guide (Vue + Bootstrap)

## 1. Project Setup:
- Install **Vue.js** and create a new Vue project called `tura`.
- Install necessary dependencies:
  - **Vue Router** (if routing is needed for multiple views).
  - **Bootstrap** using the CDN link or package manager for styling.

## 2. Bootstrap Integration:
- Add the **Bootstrap** CDN in your `index.html` file.
- Set the language to **Hungarian (hu)** and the character encoding to **UTF-8** in the `index.html`.

## 3. Vue Components Creation:
- **Create Vue Components**:
  - `Turak.vue` – This will be used for displaying and managing the tours.
  - `Jelentkezesek.vue` – This will be used for managing tour registrations.
- **App.vue**: Import both `Turak.vue` and `Jelentkezesek.vue` components.

## 4. Layout and Structure:
- Set up a **navbar** using Bootstrap components.
  - The navbar should collapse on smaller screen sizes.
  - Add logo and navigation links (Túrák, Jelentkezések, Kapcsolat).
- Make sure to apply **responsive design** using Bootstrap classes to ensure the layout adapts to different screen sizes.

## 5. UI for "Túrák" (Tours):
- On the left side, show the list of tours dynamically.
- Each tour should display a "Részletek" (details) button. Upon clicking, show/hide more information about that tour (using Vue data binding).
- Add form fields for adding a new tour (`nev`, `tav`, `elerheto_hely`), with validation for required fields.
- A **"Hozzáadás"** button should trigger a `POST` request to the backend using `fetch()`, sending the form data.

## 6. UI for "Jelentkezesek" (Registrations):
- On the left side, show the registration form.
  - Include fields for email, group size, and a dropdown list for selecting a tour. 
- Dynamically populate the dropdown list of available tours using the data from the backend (`GET` request).
- Add validation for required fields.
- Add a **"Jelentkezés"** button to send the registration data via a `POST` request to the backend.

- List all registrations on the right side with a **"Törlés"** (Delete) button next to each registration.
- When the delete button is clicked, it should trigger a `DELETE` request to remove the registration.

## 7. API Communication:
- Use the **fetch()** API to interact with the backend.
- Ensure that after a successful `POST` or `DELETE` request, the user sees a success message (use a modal, toast, or simple alert).

## 8. Additional Features:
- Use **Vue's two-way data binding** to make the UI interactive (e.g., form input).
- Handle error and success responses from the backend and show appropriate messages.
