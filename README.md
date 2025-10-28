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

