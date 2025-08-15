# flutterNewsApp: using flutter to handle API calls and UI to bring the most recent news to an enduser (API used: newsapi.org)

Project Structure
lib/core/usecase.dart # Base use case interface.
lib/core/failure.dart # Defines error handling structures.

lib/di/injector.dart # Sets up dependency injection
lib/features/app.dart # Root widgets
lib/features/main.dart # app entry point

lib/features/news/data/datasources/news_api_service.dart # Handles API calls to NewsAPI.
lib/features/news/data/models/news_api_service.dart #DTOs for parsing API responses.
lib/features/news/data/repositories #Implements domain repository interface.

lib/features/domain/entities/ # Core business models without dependencies.
lib/features/domain/repositories/ # Abstract repository contracts.
lib/features/domain/usecases/ # Business logic for fetching news.

lib/features/presentation/bloc # State management with BLoC.
lib/features/presentation/pages # UI screens.

------------------------------------------------------------------------------------------

### Clean Architecture Layers:
1. Domain Layer 
   - Contains `Entities`, `Repositories` (abstract), and `UseCases`.  
   - Independent of any frameworks or external dependencies.
   
2. Data Layer 
   - Contains `Models`, `DataSources` (API calls), and `Repository Implementations`.  
   - Converts API data to domain entities.

3. Presentation Layer
   - Handles UI and state management (BLoC).  
   - Depends only on the domain layer for business logic.

---

### SOLID Principles Applied:
- Single Responsibility — Each class has a clear, single purpose.
- Open/Closed — Code is open for extension but closed for modification.
- Liskov Substitution — Abstractions (`Repositories`) allow swapping implementations.
- Interface Segregation — Smaller, specific contracts instead of large interfaces.
- Dependency Inversion — High-level modules depend on abstractions, not concrete classes.


features/news/data/repositories/news_repository_impl.dart
•	Converts raw API data into a cleaner format (Entities) for the rest of the app. Acts as a bridge between the API service and the domain layer.
features/news/domain/repositories/news_repository.dart
•	An interface (abstract class) that lists the functions the repository should have, without deciding how they’re implemented.
features/news/domain/usecases/get_top_headlines.dart
•	Contains the business logic for “Get top headlines.” Calls the repository and returns the result in a format the UI layer can understand.
features/news/presentation/bloc/news_bloc.dart
•	Manages state and logic for the News UI. Listens for events (like “fetch headlines”) and updates the screen with loading, success, or error states.


