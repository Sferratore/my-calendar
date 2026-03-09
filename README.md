# MyCalendar

A full-stack web application built with **ASP.NET Core 6 MVC** that combines a personal calendar with real-time weather and moon phase data. Created as a learning project to explore and solidify the fundamentals of the .NET Core framework.

---

## Features

### Calendar & Annotations
Authenticated users can create, edit, and delete calendar annotations — each with a title, description, and date. Annotations are personal and tied to the logged-in user's account.

### Today's Weather
Displays current weather conditions (temperature, humidity, UV index) based on the user's location. The app geolocates the user via their IP address using the **IPinfo API**, then fetches forecast data from the **WeatherAPI**. Weather conditions are paired with custom icons for a visual overview.

### Moon Phase
Shows real-time moon data including moonrise/moonset times, current phase, and illumination percentage. Like the weather section, location is detected automatically. Each of the eight moon phases is represented by a dedicated image.

### User Authentication
Session-based registration and login system with server-side validation, duplicate email detection, and user feedback via `TempData`.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | ASP.NET Core 6 (MVC) |
| Language | C# |
| Database | SQL Server (via Entity Framework Core, code-first) |
| ORM | Entity Framework Core 6 |
| Frontend | Razor Views, Bootstrap, Bootswatch |
| APIs | WeatherAPI, IPinfo |
| Serialization | Newtonsoft.Json |

---

## Project Structure

```
MyCalendar/
├── Controllers/
│   ├── HomeController.cs           # Public pages: landing, login, register, logout
│   ├── UserSectionController.cs    # Authenticated user dashboard
│   ├── CalendarController.cs       # CRUD operations on calendar annotations
│   ├── TodayWeatherController.cs   # Weather data retrieval and processing
│   └── MoonPhaseController.cs      # Moon phase data retrieval and processing
├── Models/
│   ├── User.cs                     # User entity
│   ├── CalendarAnnotation.cs       # Calendar annotation entity (FK → User)
│   ├── *ViewModel.cs               # View models for forms and display
│   └── *ApiSettings.cs             # Strongly-typed API configuration classes
├── Views/
│   ├── Home/                       # Landing, Login, Register
│   ├── UserSection/                # User dashboard
│   ├── Calendar/                   # Index, Create, Edit
│   ├── TodayWeather/               # Weather display
│   ├── MoonPhase/                  # Moon phase display
│   └── Shared/                     # Layout, error page, validation scripts
├── Data/
│   └── ApplicationDbContext.cs     # EF Core DbContext
├── Migrations/                     # EF Core migration history
├── wwwroot/
│   ├── css/                        # Site styles + Bootswatch theme
│   ├── imgs/                       # Weather & moon phase icons
│   └── js/                         # Client-side scripts
├── Program.cs                      # App entry point & service configuration
└── appsettings.json                # Connection strings & API keys
```

---

## Prerequisites

- [.NET 6 SDK](https://dotnet.microsoft.com/download/dotnet/6.0)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/) (or SQL Server Express / LocalDB)
- A [WeatherAPI](https://www.weatherapi.com/) key
- An [IPinfo](https://ipinfo.io/) token

---

## Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/MyCalendar.git
   cd MyCalendar
   ```

2. **Configure the database and API keys**

   Edit `appsettings.json` and update the connection string to point to your SQL Server instance. Replace the API key placeholders with your own keys:
   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection": "Server=YOUR_SERVER;Database=MyCalendar;Trusted_Connection=True;"
     },
     "WeatherAPI": {
       "WeatherAPIKey": "YOUR_WEATHERAPI_KEY",
       "HistoryUrl": "http://api.weatherapi.com/v1/history.json"
     },
     "GeoIpAPI": {
       "IpAPIUrl": "http://www.ipinfo.io/",
       "IpAPIKey": "YOUR_IPINFO_TOKEN"
     }
   }
   ```

3. **Apply database migrations**
   ```bash
   dotnet ef database update
   ```

4. **Run the application**
   ```bash
   dotnet run
   ```
   The app will be available at `https://localhost:7xxx` (check console output for the exact port).

---

## Concepts & Techniques Practiced

- **MVC architecture** — clean separation of concerns across controllers, models, and Razor views
- **Dependency Injection** — services, DbContext, HttpClient, and strongly-typed configuration via `IOptions<T>`
- **Entity Framework Core** — code-first approach with migrations, navigation properties, and foreign keys
- **Data Annotations** — model validation with `[Required]`, `[StringLength]`, `[MinLength]`
- **Session management** — user authentication state stored server-side
- **External API integration** — chained async HTTP calls with `HttpClient` and JSON parsing
- **ViewModels** — dedicated models for form binding, decoupled from database entities
- **Partial views & Tag Helpers** — reusable Razor components and clean form markup
- **Server-side validation** — `ModelState` checks with user-facing error feedback

---

## License

This project is intended for educational purposes.
