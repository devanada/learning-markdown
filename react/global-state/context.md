# Global State | Context

## Table of contents

Here is an example of a plugin in action
([`remark-toc`](https://github.com/remarkjs/remark-toc)).
This section is replaced by an actual table of contents.

## Overview

Sebelumnya kita memparsing atau melemparkan sebuah data menggunakan props ke beberapa komponen yang kita buat. Namun seiring berjalannya waktu dan perkembangan aplikasi yang telah di develop membuat kita cukup menderita dan exhausted ketika masih melakukan parsing data antar komponen seperti berikut.

```javascript
import React from "react";

const App = () => {
  return (
    <div className="app">
      <SomeComponent
        user={user}
        otherProps={otherProps}
        otherPropsAgain={otherPropsAgain}
        andSomeOtherPropsPassRightHere={whatEver}
      />
    </div>
  );
};

export default App;
```

## Introducing Context

Terkadang, data dilempar dari atas ke bawah (parent to child) melalui props, namun ada beberapa kondisi dan situasi dimana terdapat sebuah data (seperti tema, pilihan bahasa) yang dibutuhkan oleh banyak komponen didalam aplikasi kita.

**Context** memberikan sebuah cara untuk melakukan passing sebuah data melalui component tree tanpa perlu passing props di setiap level.

Dengan kata lain, **Context** seperti sebuah variabel global yang bisa diakses kapanpun dan dimanapun tanpa parsing props di setiap komponen yang kita miliki.

![React Context](https://res.cloudinary.com/hypeotesa/image/upload/v1665159088/react-context-3_gvcsrj.svg "React Context")

## Kapan menggunakan Context

- Membutuhkan sebuah manajemen State yang simple
- Passing beberapa data secara mendalam tanpa perlu menggunakan Redux
- Poin plus ketika kita memiliki aplikasi dengan skala kecil ke menengah

## Apa saja penggunaan Context pada umumnya

- Global State
- Tema
- Konfigurasi aplikasi
- Username dari user yang telah login
- Pengaturan user
- Preferensi bahasa
- etc

## Langkah-langkah penggunaan **Context**

1. Buat **Context** dengan menggunakan method `createContext` lalu export

```javascript
export const MyContext = React.createContext(defaultValue);
```

2. Import **Context** yang telah dibuat sebelumnya dan bungkus component tree dengan Context Provider, dan letakkan value apapun yang kita inginkan dengan menggunakan value prop

```javascript
{/* ... */}

import { MyContext } from "../your/context/path";

function App() {
      return (
        <MyContext.Provider value={/* some value */}>
            <BrowserRouter>
                {/* other component */}
            </BrowserRouter>
        </MyContext.Provider>
      )
}
```

3. Baca value yang telah disimpan kedalam **Context** dengan menggunakan hooks `useContext`

```javascript
/* ... */

import { useContext } from "react";

import { MyContext } from "../your/context/path";

const SomeComponent = () => {
  const context = useContext(MyContext);

  /* ... */
};
```

## Kekurangan React **Context**

- Tidak direkomendasikan untuk mengkombinasikan **Context** dengan hook lain seperti **useReducer** untuk merubah sebuah nilai karena alasan performa
- Ketika nilai dari sebuah Context berubah atau diganti, maka seluruh component yang mengkonsumsi **Context** akan **re-render**
