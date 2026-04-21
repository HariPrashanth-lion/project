# Instructions

- Following Playwright test failed.
- Explain why, be concise, respect Playwright best practices.
- Provide a snippet of code with the fix, if possible.

# Test info

- Name: coursera.spec.ts >> Coursera Project
- Location: tests\coursera.spec.ts:6:5

# Error details

```
Error: locator.click: Test ended.
Call log:
  - waiting for getByRole('checkbox', { name: 'English' })

```

# Test source

```ts
  1  | import { Page } from "@playwright/test";
  2  |  
  3  | export class SearchResultsPage {
  4  |   readonly page: Page;
  5  |  
  6  |   constructor(page: Page) {
  7  |     this.page = page;
  8  |   }
  9  |  
  10 |   async filterByLanguage(language: string) {
  11 |     await this.page.getByTestId("filter-dropdown-language").click();
> 12 |     await this.page.getByRole("checkbox", { name: language }).click();
     |                                                               ^ Error: locator.click: Test ended.
  13 |     await this.page.waitForSelector("[data-testid='search-filter-group-Language']");
  14 |     const countRaw = await this.page.locator(`[data-testid='language:${language}-true'] span.css-s63saa`).textContent();
  15 |     await this.page.getByTestId("filter-view-button").click();
  16 |     return countRaw?.replace(/[()]/g, "").trim();
  17 |   }
  18 |  
  19 |   async filterByLevel(level: string) {
  20 |     await this.page.getByTestId("filter-dropdown-productDifficultyLevel").click();
  21 |     await this.page.getByRole("checkbox", { name: level }).click();
  22 |     await this.page.waitForSelector("[data-testid='search-filter-group-Level']");
  23 |     const countRaw = await this.page.locator(`[data-testid='productDifficultyLevel:${level}-true'] span.css-s63saa`).textContent();
  24 |     await this.page.getByTestId("filter-view-button").click();
  25 |     return countRaw?.replace(/[()]/g, "").trim();
  26 |   }
  27 |  
  28 |   async getCardDetails(limit: number = 2) {
  29 |     await this.page.waitForSelector("[data-testid='product-card-cds']");
  30 |     const titles = await this.page.locator("h3.cds-CommonCard-title").allTextContents();
  31 |     const ratings = await this.page.locator(".cds-RatingStat-sizeLabel .css-4s48ix").allTextContents();
  32 |     const metadata = await this.page.locator(".cds-CommonCard-metadata p.css-vac8rf").allTextContents();
  33 |  
  34 |     for (let i = 0; i < limit; i++) {
  35 |       console.log(`Card ${i + 1} title: ${titles[i]}`);
  36 |       console.log(`Card ${i + 1} rating: ${ratings[i]}`);
  37 |       console.log(`Card ${i + 1} level/duration: ${metadata[i]}`);
  38 |       console.log("-----");
  39 |     }
  40 |   }
  41 | }
```