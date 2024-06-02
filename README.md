# Let's creat a react file
># This is a React App file
```
 npx create-react-app my-app
 cd my-app
 npm start 
```
># This is a React vite
```
1. For create vite file: npm create vite@latest
2. Name of vite file: vite project (or you can click . to do not create file)
3. Select framework: React
4. Java script (or you can choose Type script)
5. cd vite project (we go into file)
6. npm install (npm i)
7. npm run dev (or can code . to go in file)
```
# Let's install libraris in our file
- You can put the link in terminal or bash
># Installing Tailwind Tailwind
```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
``` 
- put this code in Tailwind config.js file 
```
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
- put this code in index.css file
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```
- if you want to put responsive wed design size go to this link
```
https://tailwindcss.com/docs/screens
```
- At the end run your project again
># Mui (Material user interface) library
```
npm install @mui/icons-material @mui/material @emotion/styled @emotion/react
```
># Antd(design) library
```
npm i antd
```
# React dark-mode
># Dark mode Tailwind
```
npm i react-toggle-dark-mode
```
- Create hook file after useDarkSide file and put this code in useDarkSide file
```
import { useEffect, useState } from 'react';

export default function useDarkSide() {

const [theme, setTheme] = useState(localStorage.theme);
const colorTheme = theme === 'dark' ? 'light' : 'dark';

useEffect(() => {
const root = window.document.documentElement;
root.classList.remove(colorTheme);
root.classList.add(theme);

// save theme to local storage
localStorage.setItem('theme', theme);
}, 
[theme, colorTheme]);

return [colorTheme, setTheme];
}
```
- Create components and create Switcher file put this code in
```
import React, { useState } from "react";
import useDarkSide from "./Hook/useDarkSide";
import { DarkModeSwitch } from "react-toggle-dark-mode";
export default function Switcher() {
  const [colorTheme, setTheme] = useDarkSide();
  const [darkSide, setDarkSide] = useState(
    colorTheme === "light" ? true : false
  );
  const toggleDarkMode = (checked) => {
    setTheme(colorTheme);
    setDarkSide(checked);
  };
  return (
    <>
      <div>
        <DarkModeSwitch
          checked={darkSide}
          onChange={toggleDarkMode}
          size={56}
        />
      </div>
    </>
  );
}
```
- Write this in tailwind config js
```
darkMode: "class",
``` 
- Then you can import Switcher component in your app file and use dark: in your className attribute in tags
># Dark mode Mui
```
npm install @mui/material @emotion/react @emotion/styled
```
- create theme file and create theme.js file and put this code in
```
import { createTheme } from "@mui/material/styles";

// Light theme
const lightTheme = createTheme({
  palette: {
    primary: {
      main: "#A0D0D0",
      secondary: "green",
    },
    background: {
      default: "#ffffff",
    },
    text: {
      primary: "#000000",
    },
  },
});

// Dark theme
const darkTheme = createTheme({
  palette: {
    primary: {
      main: "#A0D0D0",
    },
    background: {
      default: "#121212",
    },
    text: {
      primary: "#ffffff",
    },
  },
});

export { lightTheme, darkTheme };
```
- This control your dark mode and light mode of your project
- practice this in your app file
```
import React, { useState } from "react";
import Brightness4Icon from "@mui/icons-material/Brightness4";

import {
  ThemeProvider,
  CssBaseline,
  IconButton,
  Box,
  Typography,
  Container,
  Button,
} from "@mui/material";

import { lightTheme, darkTheme } from "./theme/theme";


const App = () => {
  const storedTheme = localStorage.getItem("darkMode");

  const [darkMode, setDarkMode] = useState(storedTheme == true);

  const toggleDarkMode = () => {
    const newDarkMode = !darkMode;

    setDarkMode(newDarkMode); //
    localStorage.setItem("darkMode", newDarkMode);
  };

  const theme = darkMode ? darkTheme : lightTheme;

  return (
    <ThemeProvider theme={theme}>
      <Container>
        <CssBaseline />
        <Box sx={{ display: "flex", justifyContent: "end" }}>
          <IconButton onClick={toggleDarkMode} color="inherit">
            <Brightness4Icon />
          </IconButton>
        </Box>

        <Box>
          <Typography>MUI Theme</Typography>

          <Button>Add</Button>
        </Box>
      </Container>
    </ThemeProvider>
  );
};

export default App;
```
# Let's install animation
># Animation of texts Animate style
```
npm install animate.css --save
```
- you can put animation in class or className
```
<h1 class="animate__animated animate__bounce">An animated element</h1>
<h1 class="animate__animated animate__swing">An animated element</h1>
```
># Animation of AOS
```
npm install --save aos@next
```
- import styles in your component
```
    import AOS from 'aos';
    import 'aos/dist/aos.css';
```
- put this code into your component
```
    useEffect(() => {
        AOS.init();
    }, [])
```
># Animation of swiper
```
npm i swiper
```
- Go to this link for style
```
https://swiperjs.com/
```
># Let's install translation
- put this 3 package in your terminal or bash
```
npm i react-i18next
npm i i18next-http-backend
npm i i18next-browser-languagedetector
```
- Create a i18n file after i18next.js file and put this code in 
```
import i18next from 'i18next'
import Backend from 'i18next-http-backend'
import LanguageDetector from 'i18next-browser-languagedetector'
import { initReactI18next } from 'react-i18next'

i18next.use( Backend ).use( LanguageDetector ).use(initReactI18next).init({
  fallbackLng: 'en',
  debug: true,
  detection: {
    order: ['queryString', 'cookie'],
    cache: ['cookie']
  },
  interpolation: {
    escapeValue: false
  }
});
```
- Then create locales file in public file then create many language that you want in files create translation.json file and put your key and its translate in
![](Снимок%20экрана%202024-06-02%20172251.png)
- Import it in your app
```
import { useTranslation } from "react-i18next";
``` 
- Write this code in your component
```
  const [lng, setLng] = useState("en");
  const { t, i18n } = useTranslation();
  const changeLanguage = (language) => {
    i18n.changeLanguage(language);
  };
```
- Put this in your select
```
    <select
      value={lng}
      onChange={(event) => {
        changeLanguage(event.target.value);
        setLng(event.target.value);
      }}
    >
      <option value="en">Eng</option>
      <option value="ru">Rus</option>
    </select>
```
- When your choose one word write like this
```
    <ul className="hidden xl:flex gap-[30px]">
      <li>{t("header.nav.ul.main")}</li>
      <li>{t("header.nav.ul.about")}</li>
      <li>{t("header.nav.ul.product")}</li>
      <li>{t("header.nav.ul.process")}</li>
      <li>{t("header.nav.ul.reliability")}</li>
      <li>{t("header.nav.ul.client")}</li>
    </ul>
```
># Install filebase64
```
npm i react-file-base64
```
- Import it
```
import FileBase64 from 'react-file-base64';
```
- Put component
```
    <FileBase64
    multiple={ true }
    onDone={ this.getFiles.bind(this) } />
```
># Install formik
```
npm install formik --save
```
- Validation of formim (yup)
```
npm install formik yup
```










start from router