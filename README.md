# 🎬 IMovies — Full-Stack MERN Movie Ticket Booking Platform

**IMovies** is a full-featured, modern movie ticket booking web application built on the MERN stack (MongoDB, Express.js, React.js, Node.js) with Vite, Bootstrap 5, and JWT authentication.

---

## 🌟 Key Features

1. **Movie Catalog & Premiere Showcase**:
   - Hero spotlight for trending releases with backdrop imagery.
   - Filter movies by Genre (Action, Sci-Fi, Adventure, Drama, Animation, etc.) and search by title.
   - Comprehensive movie details including duration, language, IMDb-style rating, synopsis, director, cast, and trailer link.

2. **Theatres, Screen Formats & Showtimes**:
   - Multi-day showtime scheduling (Today, Tomorrow, and upcoming dates).
   - Grouped screenings by cineplex (e.g. *PVR ICON: Gold Class*, *INOX Megaplex*, *Cinepolis IMAX 3D*).
   - Screen format indicators (IMAX 3D, 2D, 3D, 4DX).

3. **Interactive Visual Seat Booking Engine**:
   - Realistic cinema seating layout with curved screen projection indicator.
   - Tiered seating structure:
     - **VIP Tier** (Rows A-B)
     - **Premium Tier** (Rows C-E)
     - **Regular Tier** (Rows F-H)
   - Real-time seat status indicators: Available, Selected (Neon glow), and Booked/Sold Out (dimmed).
   - Double-booking prevention with collision validation.

4. **Digital Cinema E-Ticket & Checkout**:
   - Live price calculator itemizing ticket tiers, convenience fee, and GST.
   - Instant ticket generation with booking reference code, hall & seat details, and scannable QR placeholder.
   - Direct Print / Save ticket option (`window.print()`).

5. **User & Admin Management**:
   - Secure user authentication with password hashing (`bcryptjs`) and JWT tokens.
   - **My Bookings** dashboard allowing users to view tickets and cancel reservations with instant seat release.
   - **Admin Control Panel**: Add new movies, schedule showtimes across theatres, and view platform-wide bookings and ticketing revenue.

---

## 🔑 Quick-Testing Accounts

| Role | Email | Password |
|---|---|---|
| **Admin** | `admin@imovies.com` | `admin123` |
| **Demo Customer** | `demo@imovies.com` | `demo123` |

*(The Sign-In page also includes 1-click autofill buttons for these credentials!)*

---

## 🚀 How to Run Locally

**Prerequisites:** Node.js 20+ and npm.

### 1. Install Dependencies
```bash
cd backend && npm install
cd ../frontend && npm install
```

### 2. Start the Backend Server (Port 5000)
Open a terminal in the project directory:
```bash
cd backend
npm run dev
```
> The API will listen on `http://localhost:5000/api` with hot-reloading via `nodemon`.

### 3. Start the Frontend Application (Port 5173)
In a second terminal:
```bash
cd frontend
npm run dev
```
> Open your browser and navigate to **`http://localhost:5173`**. Vite proxies `/api` requests to `http://localhost:5000`.

### ⚠️ macOS: Port 5000 Already in Use
On macOS, port 5000 is taken by the **AirPlay Receiver** (`ControlCenter`), so the backend can't bind to it. Either turn off AirPlay Receiver in *System Settings → General → AirDrop & Handoff*, or run the backend on another port and point the frontend at it:
```bash
# Terminal 1
cd backend
PORT=5001 npm run dev

# Terminal 2
cd frontend
VITE_API_BASE_URL=http://localhost:5001/api npm run dev
```
> The backend allows all CORS origins, so the frontend can call it directly.

---

## 🌐 Database Configuration (MongoDB Atlas)

`backend/.env` is **not** in the repository (it's gitignored). Without it, the backend starts with the built-in in-memory database (see the note below). To connect to MongoDB, create `backend/.env`:
```env
PORT=5000
MONGODB_URI=mongodb+srv://<user>:<password>@<cluster>.mongodb.net/imovies?retryWrites=true&w=majority
JWT_SECRET=<your-secret>
```
> If `JWT_SECRET` is not set, the backend falls back to an insecure default secret. Always set it outside local testing.

### Whitelisting your IP in MongoDB Atlas:
To allow your machine to connect directly to the Atlas cluster:
1. Log into your [MongoDB Atlas Console](https://cloud.mongodb.com/).
2. Navigate to **Network Access** under Security.
3. Click **Add IP Address** -> select **Allow Access from Anywhere** (`0.0.0.0/0`) or add your current public IP.
4. Click **Confirm**.

> **Note**: If there's no `MONGODB_URI` or Atlas can't be reached (e.g. your IP isn't whitelisted), the backend falls back to a built-in in-memory database with 12 movies, 36 showtimes, and the seed accounts above, so you can test every feature. Data you create in this mode is lost when the backend restarts. Check which mode is active at `http://localhost:5000/api`.
