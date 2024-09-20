# Projectoverzicht

![image](https://github.com/user-attachments/assets/a948d273-ba5d-4851-a49d-11bab71381b6)


Dit project integreert **Prismic CMS** met een **SvelteKit** front-end, waardoor dynamisch contentbeheer mogelijk is via Prismic's **Slices**. Slices maken het mogelijk om herbruikbare, flexibele contentblokken te gebruiken, waardoor het eenvoudig is om content te maken en bij te werken zonder dat de code aangepast hoeft te worden.

## 1. Prismic CMS Setup

Het project gebruikt een aangepast contenttype in Prismic genaamd `page`. Dit contenttype is als volgt gestructureerd:

- **UID**: Een unieke identificator die wordt gebruikt voor routing.
- **Naam**: Een tekstveld om de naam van de pagina op te slaan.
- **Slice Zone**: Een flexibel gebied waar editors verschillende slices (herbruikbare contentblokken) kunnen toevoegen.
- **SEO & Metadata**: Velden voor SEO-optimalisatie, inclusief meta titel, beschrijving en een afbeelding voor social sharing.

Hier is hoe dit type is gedefinieerd in Prismic (`index.json`):

```
{
  "id": "page",
  "label": "page",
  "format": "page",
  "repeatable": true,
  "status": true,
  "json": {
    "Main": {
      "uid": {
        "config": {
          "label": "UID"
        },
        "type": "UID"
      },
      "name": {
        "type": "Text",
        "config": {
          "label": "name"
        }
      },
      "slices": {
        "type": "Slices",
        "fieldset": "Slice Zone",
        "config": {
          "choices": {
            "page_content": {
              "type": "SharedSlice"
            },
            "test_slice": {
              "type": "SharedSlice"
            }
          }
        }
      }
    },
    "SEO & Metadata": {
      "meta_description": {
        "config": {
          "label": "Meta Description",
          "placeholder": "Een korte samenvatting van de pagina"
        },
        "type": "Text"
      },
      "meta_image": {
        "config": {
          "constraint": {
            "height": 1260,
            "width": 2400
          },
          "label": "Meta Image"
        },
        "type": "Image"
      },
      "meta_title": {
        "config": {
          "label": "Meta Title"
        },
        "type": "Text"
      }
    }
  }
}
```

## 2. Slices in het Project
Slices zijn herbruikbare contentblokken die editors dynamisch kunnen toevoegen aan de pagina. Dit project bevat twee hoofd-slices:

PageContent Slice

De PageContent slice toont een eenvoudige kop. Hier is hoe de slice wordt gerenderd in de Svelte-component:
```
<script>
  /** @type {import("@prismicio/client").Content.PageContentSlice} */
  export let slice;
</script>

<section data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
  <h1>{slice.primary.textfield}</h1>
</section>

<style>
  h1 {
    color: #333;
    font-size: 2rem;
    text-align: center;
    margin: 4rem;
  }
</style>
```

Mock Data (mocks.json) simuleert de inhoud van deze slice voor lokale ontwikkeling:
```
[
  {
    "variation": "default",
    "primary": {
      "textfield": {
        "value": "tussen"
      }
    },
    "items": []
  }
]
```

TestSlice

De TestSlice slice toont een galerij van afbeeldingen. Hier is hoe de slice wordt gerenderd:
```
<script>
  import { PrismicImage } from '@prismicio/svelte';
  export let slice;
</script>

<section data-slice-type={slice.slice_type} data-slice-variation={slice.variation}>
  {#each slice.items as item}
    <PrismicImage field={item.imagefield} width="200" height="300" />
  {/each}
</section>

<style>
  section[data-slice-type] {
    display: flex;
    flex-direction: column;
    gap: 20px;
    padding: 20px;
    background-color: #002b5b;
  }
</style>
```
Mockdata voor deze slice (mocks.json):
```
[
  {
    "variation": "default",
    "items": [
      {
        "imagefield": {
          "url": "https://images.unsplash.com/photo-1560762484-813fc97650a0",
          "width": 3344,
          "height": 2509
        }
      }
    ]
  }
]
```

## 3. Gegevens ophalen uit Prismic

De app gebruikt de Prismic-client om paginagegevens op te halen uit de CMS. Dit is ingesteld in prismicio.js:
```
import * as prismic from '@prismicio/client';
import config from '../../slicemachine.config.json';

export const repositoryName = config.repositoryName;

export const createClient = (config = {}) => {
  const client = prismic.createClient(repositoryName, { ...config });
  return client;
};
```
## 4. Het Weergeven van de Slices

Zodra de content is opgehaald uit Prismic, worden de slices dynamisch gerenderd met behulp van de SliceZone-component in Svelte:
```
<script>
  import { SliceZone } from '@prismicio/svelte';
  import { components } from '$lib/slices';
  export let data;
</script>

<article>
  <SliceZone slices={data.slices} {components} />
  <header>
    <h1>{data.name}</h1>
    <p><em>Tweede jaar Front-end Developer</em></p>
    <h2>Klasse 1998 <br /> Geborteplaats : Napels</h2>
  </header>
</article>
```
## 5. Ontwikkeling met de Slice Simulator

De Slice Simulator helpt ontwikkelaars om slices lokaal te testen zonder dat echte content van Prismic nodig is. De simulator is gedefinieerd in slice-simulator.svelte:
```
<script>
  import { SliceSimulator } from '@slicemachine/adapter-sveltekit/simulator';
  import { SliceZone } from '@prismicio/svelte';
  import { components } from '$lib/slices';
</script>

<SliceSimulator let:slices>
  <SliceZone {slices} {components} />
</SliceSimulator>
```
Hiermee kun je tijdens de ontwikkeling testen hoe slices worden gerenderd met mockdata.


## 6. Paginavoorbeeld

De hoofdpagina is gestructureerd met slices, waardoor de content dynamisch kan worden gegenereerd en gerenderd op basis van de gegevens uit Prismic. De layout is eenvoudig en responsief, met de nadruk op belangrijke vaardigheden en hobby’s.

Hier is een fragment uit index.svelte:
```
<body>
  <article>
    <header>
      <h1>{data.name}</h1>
      <h2>Geborteplaats: Napels</h2>
    </header>
    <div class="skills">
      <h1>Mijn Skills</h1>
      <ul>
        <li>Ik spreek vloeiend Italiaans, Spaans, Frans, Nederlands en Engels.</li>
        <li>Nu leer ik programmeertalen zoals JavaScript en compilers zoals Svelte-Kit.</li>
      </ul>
    </div>
    <div class="hobbies">
      <h1>Mijn Hobbies</h1>
      <ul>
        <li>Ik houd van zingen, dansen, zeilen, reizen en tekenen.</li>
      </ul>
    </div>
  </article>
</body>
```
## 7. Het Project Uitvoeren

Volg deze stappen om het project uit te voeren:

	1.	Clone de repository.
	2.	Installeer de afhankelijkheden: npm install.
	3.	Stel de Prismic-repository en slices in met Slice Machine.
	4.	Start de ontwikkelserver: npm run dev.

Deze README biedt een overzicht van hoe de app interacteert met Prismic, hoe slices worden behandeld en hoe dynamische content wordt gerenderd met Svelte.









# create-svelte

Everything you need to build a Svelte project, powered by [`create-svelte`](https://github.com/sveltejs/kit/tree/master/packages/create-svelte).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project in the current directory
npm create svelte@latest

# create a new project in my-app
npm create svelte@latest my-app
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.
