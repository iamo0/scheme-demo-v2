# REST 

## События
### /events
- GET
Response:
```js
[
  {
    name: string,
    date: number,
    event_url: string,
  }
]
```

- POST - создает новое событие
Request:
```js
[
  {
    name: string,
    date: number,
    hall_url: string,
    price_scheme: string,
  }
]
```

Response
200
JSON созданного события

### /event/${id}
- GET
- UPDATE
- DELETE

```js
{
  id: string,
  name: string,
  date: number,
  hall_url: string,
  price_scheme_url: string,
  available_tickets_url: string
}
```

## Залы
### /halls/
- GET — список всех залов
Response
```js
[
  {
    id: string,
    name: string,
    url: string,
  }
]
```

- POST
Request — создает запись в /halls, /halls/${id}/visual, и /price_schemes
Response 
200 
JSON созданного зала 

### /halls/{$id}
- GET
- UPDATE
- DELETE — удаляет сразу же /halls/${id}/visual и /price_schemes/{$id}

```js
{
  id: string,
  visual_url: string, // /halls/${id}/visual
  price_schemes_urls: string[],
  
  // Остальная модель остается как есть, интерфейс hall.ts
  name: string,
  sections: {
    [ID: string]: Section
  },
  rows: {
    [ID: string]: Row
  },
  seats: {
    [ID: string]: Seat
  }
}
```

### /halls/${id}/visual
- GET
- UPDATE

```js
// Интерфейс из hallVisual.ts
```

## Распоясовки
### /price-schemes
- GET
* Отдельный POST пока не нужен, потому что POST на /halls/ создает сразу и распоясовки

```js
[
  {
    id: string,
    hall_url: string,
    url: string
  }
]
```

### /price-schemes/${id}
- GET
- UPDATE

```js
{
  id: string,
  hall_url: string,
  seats_prices_url: string,

  // Интерфейс из priceSchemes.ts
  [ID: string]: {
    name: string,
    groups: {
      [GroupID: string]: {
        color: string,
        price: number
      }
    },

    // Интерфейс из sectionsPrices.ts (есть смысл смерджить эти две сущности)
    seats-prices: {
      [SeatID: string]: [GroupID: string]
    }
  }
}
```
