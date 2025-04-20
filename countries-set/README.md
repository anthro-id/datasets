# Countries Set
This is our simplified version, sets of listed countries (including common name and ISO 3166 Alpha 2 code)

# Resources/Citations
- https://gitlab.com/restcountries/restcountries/-/blob/master/src/main/resources/countriesV3.1.json

# Filtering
Some countries were filtered due to safety reasons and it must comply with our [Terms of Use](https://github.com/anthro-id/legal/blob/preview/en-US/TERMS-OF-USE.md#5-use-of-the-platform-outside-indonesia).

We use this code (in vanilla JavaScript) to filter these countries from our registry.

```js
const req = await fetch("https://restcountries.com/v3.1/all?fields=cca2,name");
  
const data = await req.json() as Array<{ cca2: string, name: Record<"common" | "official", string> }>;
  
return data
  .map(({name, cca2}) => ({cca2, name: name.common}))
  .filter(({cca2}) => !["BY", "CU", "IR", "IL", "KP", "RU", "SY", "VE", "XX", "T1"].includes(cca2))
  .sort((a, b) => a.name.localeCompare(b.name));
```