# 📅 Schema vecka 7: Interaktivitet & Arkitektur

Den här veckan går vi från att bara "titta" på data till att faktiskt interagera med den. Vi ska lära oss den viktiga balansen mellan **Server** och **Client** och hur vi skapar egna beckend med **API Routes**.

---

## 📅 Måndag: Server vs Client & API Routes

Vi går direkt på djupet genom att bygga en interaktiv "Gilla-funktion". Vi lär oss hur Next.js delar upp arbetet mellan servern och webbläsaren och hur vi pratar med vår egen backend.

Client vs Server

![Server vs Client - från https://levelup.gitconnected.com/next-js-client-side-and-server-side-components-when-and-what-to-use-7c4beccf1eab](https://miro.medium.com/v2/resize:fit:720/format:webp/1*n-TVYb7Hu1LswYOXm2OnzA.png)

Rendering Lifecycle of Server and Client (från https://javascript.plainenglish.io/next-js-15-tutorial-part-38-rendering-lifecycle-of-server-and-client-components-7a80006e14a2)

![Rendering Lifecycle of Server and Client ](https://miro.medium.com/v2/resize:fit:1400/1*AQ1bKekPg_DBR1zDog_MaA.png)

### Mål för dagarna

* **The Mental Model:** Förstå när koden körs på servern (SEO/Säkerhet) och när den körs i webbläsaren (Interaktivitet).
* **"Use Client":** Lära oss att sätta gränser för vår JavaScript-mängd.
* **Hooks & State:** Använda `useState` för att hantera klick och datahämtning på klientsidan.
* **API Routes:** Bygga egna endpoints i `/api` för att hantera POST- och GET-anrop.
* **Optimering:** Minska mängden JavaScript som skickas till klienten.

### Live-kodning: "The Like System"

Vi bygger ett system där man kan gilla karaktärer eller produkter.

1. Vi skapar en **Server Component** som hämtar grunddatan.
2. Vi skapar en **Client Component** (`LikeButton`) med `useState`.
3. Vi bygger en **Route Handler** (`api/like/route.ts`) som fungerar som vår mini-backend.

### Läsning
* Läs gärna igenom denna innan föreläsningen om ni kan - [Server and Client Components](https://nextjs.org/docs/app/getting-started/server-and-client-components)
* [React Docs: Server components](https://react.dev/reference/rsc/server-components)
* [React Docs: "use client"](https://react.dev/reference/rsc/use-client)
* [Next.js Docs: Route Handlers (API)](https://nextjs.org/docs/app/building-your-application/routing/route-handlers)
* [React Docs: useState](https://react.dev/reference/react/useState)

---

## 📅 Tisdag: URL State Management i med Cliend components

Vi tar vidare det vi arbetat med i server med searchParams, men flyttar in vissa delar in i client components. Vi gör om våra hårdkodade länkar för limit osv till interaktiva element. 

### Mål för dagen

* **searchParams:** Läsa filter och sökord direkt från URL:en.
* **useRouter & usePathname:** Navigera programmatiskt när användaren klickar eller skriver.
* **Persistens:** Varför URL-state ofta är bättre än vanlig `useState` för filtrering.
* **Leaf Components:** Att hålla sina Client Components små och placerade längst ut i komponentträdet.

### Läsning

* [Next.js Docs: useSearchParams](https://nextjs.org/docs/app/api-reference/functions/use-search-params)
* [Next.js Docs: useRouter](https://nextjs.org/docs/app/api-reference/functions/use-router)

---

## 📅 Onsdag & Torsdag: Repetition


### Mål för dagen
* Jobba vidare med det ni lärt er senaste veckorna. Lägg gärna lite tid på e-learning också!

---

## 📅 Fredag: Code Review & Reflektion

Vi snyggar till koden och kollar på varandras lösningar från veckans projekt.

### Frågor för Code Review

* Har vi placerat `"use client"` på rätt ställe, eller "smittar" den för mycket av appen?
* Fungerar vår API-route även om vi laddar om sidan?
* Hur känns prestandan i Network-tabben?

---

## 🛒 Veckans Projekt: The Modern Store (Interaktiv)

Fortsätt på din webshop från förra veckan, men lägg till följande:

1. **Gilla-funktion:** Implementera en `LikeButton` på dina produkter som pratar med en API-route.
2. **URL-Filter:** När man väljer en kategori eller söker ska URL:en uppdateras (t.ex. `?category=electronics`).
3. **Optimering:** Se till att så mycket som möjligt av din produktvisning sker i Server Components.

### Exempel på API-Route för Likes:

```typescript
// app/api/like/route.ts
import { NextResponse } from "next/server"

const likesStore = new Map<string, number>()

export async function POST(request: Request) {
    const { characterName } = await request.json()
    const currentLikes = likesStore.get(characterName) || 0
    const newLikes = currentLikes + 1
    likesStore.set(characterName, newLikes)

    return NextResponse.json({ likes: newLikes })
}

```

---

## 📚 Extra material & E-learning

* [Next.js Tutorial: Client vs Server Components](https://www.google.com/search?q=https://www.youtube.com/watch%3Fv%3DkaS7it45vX0)
* [ByteGrad: Next.js API Routes Explained](https://www.youtube.com/watch?v=KAQCHfu_3jw)
