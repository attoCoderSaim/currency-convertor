# Currency Converter App

This project is a React-based currency converter that uses a custom hook `useCurrencyInfo` to fetch real-time exchange rates and convert between different currencies.

## Features
- Fetches real-time currency exchange rates
- Converts one currency to another
- Uses a custom React hook for data fetching
- Simple and user-friendly UI

## Installation
Ensure you have Node.js installed. Then, install dependencies:

```sh
npm install
```

## Usage

### Import the Hook
```js
import useCurrencyInfo from "./useCurrencyInfo";
```

### Use in a React Component
```js
import React, { useState } from "react";
import useCurrencyInfo from "./useCurrencyInfo";

function CurrencyConverter() {
    const [amount, setAmount] = useState(1);
    const [fromCurrency, setFromCurrency] = useState("usd");
    const [toCurrency, setToCurrency] = useState("eur");
    const currencyData = useCurrencyInfo(fromCurrency);

    const convertedAmount = currencyData ? (amount * currencyData[toCurrency]).toFixed(2) : "Loading...";

    return (
        <div>
            <h2>Currency Converter</h2>
            <input 
                type="number" 
                value={amount} 
                onChange={(e) => setAmount(e.target.value)} 
            />
            <select value={fromCurrency} onChange={(e) => setFromCurrency(e.target.value)}>
                <option value="usd">USD</option>
                <option value="eur">EUR</option>
                <option value="gbp">GBP</option>
            </select>
            <span> to </span>
            <select value={toCurrency} onChange={(e) => setToCurrency(e.target.value)}>
                <option value="usd">USD</option>
                <option value="eur">EUR</option>
                <option value="gbp">GBP</option>
            </select>
            <h3>Converted Amount: {convertedAmount} {toCurrency.toUpperCase()}</h3>
        </div>
    );
}

export default CurrencyConverter;
```

## Hook Implementation
```js
import { useEffect, useState } from "react";

function useCurrencyInfo(currency) {
    const [data, setData] = useState(null);

    useEffect(() => {
        fetch(`https://cdn.jsdelivr.net/npm/@fawazahmed0/currency-api@latest/v1/currencies/${currency}.json`)
            .then((res) => res.json())
            .then((res) => {
                setData(res[currency]);
            })
            .catch((error) => console.error("Error fetching data:", error));
    }, [currency]);

    return data;
}

export default useCurrencyInfo;
```

## API Used
- **[Fawaz Ahmed's Currency API](https://github.com/fawazahmed0/currency-api)**

## Requirements
- React 18+
- Node.js 14+

## Running the Project
```sh
npm start
```

## License
This project is open-source and available under the MIT License.

