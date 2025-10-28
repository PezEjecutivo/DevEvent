 Enlace a la web:
 Enlace al repositorio:

---

Creamos un proyecto de Next.js 16, [pagina oficial](https://nextjs.org/)  (En caso de que Next.js ya no sea la ultima versión, solo tendreis que cambiar el @latest por la versión que quieras)

```bash
npx create-next-app@latest
```

Una vez usemos ese comando, nos preguntara que tipo de configuración queremos, en nuestro caso utilizaremos la configuración recomendada, la cual esta configurada con: `TypeScript, ESLint, Tailwind CSS, App Router, Turbopack`.

Para comprobar que hemos creado el proyecto sin problemas, utilizaremos el comando `npm run dev`, si vamos al puerto 3000 de nuestro local host podremos ver que esta la pagina por defecto de Nextjs

Aunque TailwindCSS viene instalado (debido a la configuración que hemos escogido) tambien necesitaremos instalar `tw-animate-css`, para ello, tendremos que usar el siguiente comando:

```shell
npm install --save-dev tw-animate-css
```

Una vez tenemos todas las dependencias que necesitamos instaladas y cambiado el favicon de la carpeta `app`, necesitaremos cambiar el titulo de la pagina, para cambiarlo tendremos que ir a `app > layout.tsx` y modificar la metadata:

```typescript
export const metadata: Metadata = {
  title: "DevEvent",
  description: "The Hub for Every Dev Event You Mustn't Miss",
};
```

Además de esto, como vamos a utilizar diferentes tipografias, tendremos que cambiarlas/importarlas en el mismo archivo, es decir `app > layout.tsx`, las tipografias que vamos a usar seran: **Schibsted_Grotesk** y **Martian_Mono**, una vez hemos cambiado las tipografias y los metadatos, nuestos layout.tsx deberia verse tal que así:

```typescript
import type { Metadata } from "next";
import { Schibsted_Grotesk, Martian_Mono } from "next/font/google";
import "./globals.css";

const schibstedGrotesk = Schibsted_Grotesk({
  variable: "--font-schibsted-grotesk",
  subsets: ["latin"],
});

const martianMono = Martian_Mono({
  variable: "--font-martian-mono",
  subsets: ["latin"],
});

export const metadata: Metadata = {
  title: "DevEvent",
  description: "The Hub for Every Dev Event You Mustn't Miss",
};

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="en">
      <body
        className={`${schibstedGrotesk.variable} ${martianMono.variable} min-h-screen antialiased`}
      >
        {children}
      </body>
    </html>
  );
}
```

---

## React bits - Light Rays
Este es un componente que vamos a utilizar para crear una ambientación y mejorar la experiencia del usuario en la pagina, este es el enlace a la [web oficial](https://www.reactbits.dev/backgrounds/light-rays). Una vez en la pagina, cambiaremos de preview a code y pondremos CLI en vez de manual, una vez hecho eso, solo tenemos que seguir los pasos que nos indica para instalarlo:

```shell
npx shadcn@latest add https://reactbits.dev/r/LightRays-JS-CSS
```

Cuando pongamos ese comando, nos preguntara varias cosas a las que tenemos que decirle que si (y), las cuales son sin queremos instalar `shadcn` y si queremos crear `components.json`. Una respondido afirmativamente a esas preguntas, nos preguntara por el color, el cual escogeremos el neutro (neutral).

Una vez hemos hecho eso, crearemos la mitica carpeta de `components` y añadiremos `LightRays.tsx`, y pondremos el codigo que nos ofrece el componente, para nuestras especificaciones (TypeScript y TailwindCSS).

A la hora de utilizarlo, no lo vamos a utilizar en un archivo `page.tsx`, ya que lo usaremos en el layout global, para que este esté efecto en todas y cada una de las paginas, haciendo que sea más consistente y optimizado, ya que solamente lo usaremos una vez, y no una vez por cada pagina.

Una vez estamos en el `app > layout.tsx`, justo al principio del body, utilizaremos el componente, para usarlo, simplemente tendremos que pegar el apartado de `Usage` de la pagina y asegurarnos de que hemos importado bien el componente, en nuestro caso, como no necesitamos el div, podemos borrarlo y le cambiaremos el color a `#5dfeca`.

Nuestro root-layout deberia de verse de esta manera:

```typescript
import type { Metadata } from "next";
import { Schibsted_Grotesk, Martian_Mono } from "next/font/google";
import "./globals.css";
import LightRays from "@/components/LightRays";

const schibstedGrotesk = Schibsted_Grotesk({
  variable: "--font-schibsted-grotesk",
  subsets: ["latin"],
});

const martianMono = Martian_Mono({
  variable: "--font-martian-mono",
  subsets: ["latin"],
});

export const metadata: Metadata = {
  title: "DevEvent",
  description: "The Hub for Every Dev Event You Mustn't Miss",
};

export default function RootLayout({
  children,
}: Readonly<{
  children: React.ReactNode;
}>) {
  return (
    <html lang="en">
      <body
        className={`${schibstedGrotesk.variable} ${martianMono.variable} min-h-screen antialiased`}
      >
        <LightRays
          raysOrigin="top-center-offset"
          raysColor="#5dfeca"
          raysSpeed={1.5}
          lightSpread={0.8}
          rayLength={1.2}
          followMouse={true}
          mouseInfluence={0.1}
          noiseAmount={0.1}
          distortion={0.05}
          className="custom-rays"
        />
        {children}
      </body>
    </html>
  );
}
```

Una vez tenemos el componente funcionando, deberemos de cambiarle algunas propiedades para hacer la animación más simple y elegante, ya que al ser una animación que sigue a tu ratón, es importante que se note pero no demasiado, ya que queremos que la gente vea la pagina, no que se ponga a jugar con la animación.

Los cambios son los siguientes:

```typescript
        <LightRays
          raysOrigin="top-center-offset"
          raysColor="#5dfeca"
          raysSpeed={0.5}
          lightSpread={0.9}
          rayLength={1.4}
          followMouse={true}
          mouseInfluence={0.02}
          noiseAmount={0.0}
          distortion={0.01}
        />
```

Ahora, ademas de esto, lo vamos a meter en un div (tal y como estaba al principio) para darle nuestros estilos propios, tales como:

- absolute: para que no interactue con ningun otro elemento de la pagina
- inset-0: para que ocupe todo del contenedor
- top-0: para que empiece arriba del todo
- z-\[-1\]: para que este atras del todo
- min-h-screen: para que pille el tamaño de toda la pagina

Además de esto, pondremos al objeto en un main, en vez de dejarlo sin nada como estaba antes:

```typescript
        <div className="absolute inset-0 top-0 z-[-1] min-h-screen">
          <LightRays
            raysOrigin="top-center-offset"
            raysColor="#5dfeca"
            raysSpeed={0.5}
            lightSpread={0.9}
            rayLength={1.4}
            followMouse={true}
            mouseInfluence={0.02}
            noiseAmount={0.0}
            distortion={0.01}
          />
        </div>
        <main>
          {children}
        </main>
      </body>
```

