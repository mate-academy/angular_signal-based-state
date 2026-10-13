# Moonbase Control: Stan oparty o sygnały

Zadanie z modułu Angular. Repozytorium zawiera kod startowy aplikacji Moonbase Control dla tej lekcji.

## Zadanie

#### Podłącz pozostałe karty Dashboardu do rzeczywistych danych
Karty `Total Missions` i `Active Missions` wykorzystują już wartości wyliczane na podstawie danych z `MissionsService`. Karty dotyczące incydentów nadal zawierają wartości wpisane na stałe.

Rozszerz aplikację o dane dotyczące incydentów i wykorzystaj je w Dashboardzie.

#### 1. Utwórz model danych dla incydentów
W folderze `features/incidents`:

- utwórz enum `IncidentSeverity`,
- utwórz interface `Incident`,
- wykorzystaj `IncidentSeverity` jako typ pola `severity`.

```
export enum IncidentSeverity {
  Low = 'low',
  Medium = 'medium',
  High = 'high',
  Critical = 'critical',
}
```

```
export interface Incident {
  title: string;
  description: string;
  severity: IncidentSeverity;
}
```

#### 2. Utwórz `IncidentsService`
W folderze `features/incidents` utwórz `IncidentsService` zgodnie z tym samym wzorcem, który został wykorzystany w `MissionsService`.

Serwis powinien:

- używać dekoratora `@Service()`,
- przechowywać stan danych w prywatnym `httpResource<Incident[]>`,
- pobierać dane z endpointu `http://localhost:4000/incidents`,
- ustawiać pustą tablicę jako `defaultValue`,
- udostępniać dane na zewnątrz przez `asReadonly()`.
Struktura serwisu powinna odpowiadać strukturze `MissionsService`.

#### 3. Podłącz dane do Dashboardu
- wstrzyknij `IncidentsService` do komponentu `Dashboard`,
- wykorzystaj dane z serwisu jako źródło informacji dla kart dotyczących incydentów.

#### 4. Dodaj wartości wyliczane
Utwórz sygnały `computed()`, które będą wyliczały:

- całkowitą liczbę incydentów,
- liczbę incydentów, których `severity` ma wartość `IncidentSeverity.Critical`.

#### 5. Zaktualizuj UI
Podłącz wyliczone wartości do kart:

- Total Incidents,
- Critical Incidents.
Sprawdź, czy wartości kart odpowiadają danym pobranym przez `IncidentsService`.

#### Efekt
`IncidentsService` korzysta z tego samego wzorca zarządzania danymi co `MissionsService`, a Dashboard pobiera dane z dwóch niezależnych serwisów i wylicza wartości kart za pomocą `computed()`.

## Jak zacząć

1. Zrób fork tego repozytorium na swoje konto GitHub.
2. Sklonuj swój fork na komputer.
3. Zainstaluj zależności: `npm install`.
4. Uruchom aplikację: `npm start`.
5. Jeśli zadanie korzysta z danych z API, uruchom w drugim terminalu mock API: `npm run api`.

## Jak oddać zadanie

1. Zapisz zmiany w commicie i wypchnij je do swojego forka.
2. Otwórz Pull Request z forka do repozytorium `mate-academy/angular_signal-based-state`, do brancha `main`.
3. Platforma uruchomi review Twojego Pull Requesta.
