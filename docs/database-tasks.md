# Database Task Guide (MySQL)

## 1. Set up Database:
- Install MySQL locally (or use an existing MySQL database).
- Create a new database called `tura_db` with **UTF-8 encoding** and **Hungarian collation** (e.g., `utf8mb4_hungarian_ci`).
- Make sure the database is properly configured to handle special characters.

## 2. Create Tables:
- **`turak` Table (for Tours)**:
  - Fields: `id` (auto-increment), `nev` (name), `tav` (distance in km), `elerheto_hely` (available spots).
  - `id` will be the primary key.
- **`jelentkezesek` Table (for Registrations)**:
  - Fields: `id` (auto-increment), `tura_id` (foreign key linked to `turak.id`), `email`, `letszam` (group size).
  - `id` will be the primary key, and `tura_id` will be the foreign key referencing the `turak` table.

## 3. Relationships:
- Define the relationship between the `turak` and `jelentkezesek` tables:
  - Each **tour** can have multiple **registrations** (one-to-many).
  - Ensure referential integrity using foreign keys.

## 4. Sample Data:
- Insert some sample tour data into the `turak` table (e.g., "Téli Mátra", "Hegyek túra", etc.).
- Insert some sample registrations in the `jelentkezesek` table with corresponding `tura_id`.

## 5. Validation:
- Ensure the database validates the **availability of spots** when a registration is added.
- Use database queries to check if the available spots (`elerheto_hely`) are sufficient for the requested number of participants before adding a new registration.
