# Auth con firebase

# Configuración de Firebase en la Consola
## Crea una cuenta de Firebase: Ve al sitio web de Firebase (https://firebase.google.com/) y crea una cuenta utilizando tu cuenta de Google.

## Crea un proyecto de Firebase: Una vez que hayas iniciado sesión, haz clic en "Crear un proyecto" y sigue las instrucciones para crear un nuevo proyecto de Firebase. Elige un nombre para el proyecto y selecciona la ubicación geográfica más cercana.

## Activa los servicios de Firebase: Dependiendo de las funcionalidades que necesites para tu aplicación, activa los servicios relevantes en la sección "Desarrollar" de tu proyecto de Firebase. Por ejemplo, puedes activar Firebase Authentication si necesitas autenticación de usuarios, Firebase Cloud Firestore si necesitas una base de datos en tiempo real, etc.

## Obtén las credenciales: Para conectar tu aplicación React Native con Firebase, necesitarás las credenciales del proyecto. Ve a la sección "Configuración del proyecto" y selecciona la pestaña "General". Aquí encontrarás las credenciales que necesitas, como el SDK de Firebase para la configuración en React Native.

# Configuración de Firebase en React Native

## Configuración en el punto de entrada: En el archivo App.js (o el punto de entrada de tu aplicación), importa y configura Firebase utilizando las credenciales que obtuviste de la consola de Firebase:

```jsx
import React from 'react';
import { AppRegistry } from 'react-native';
import App from './App';
import { name as appName } from './app.json';
import firebase from '@react-native-firebase/app';

const firebaseConfig = {
  apiKey: 'TU_API_KEY',
  authDomain: 'TU_AUTH_DOMAIN',
  projectId: 'TU_PROJECT_ID',
  storageBucket: 'TU_STORAGE_BUCKET',
  messagingSenderId: 'TU_MESSAGING_SENDER_ID',
  appId: 'TU_APP_ID',
};

if (!firebase.apps.length) {
  firebase.initializeApp(firebaseConfig);
}

AppRegistry.registerComponent(appName, () => App);
```

## Uso de Firebase en la aplicación: Ahora que Firebase está configurado, puedes utilizar sus diferentes servicios en tu aplicación. Por ejemplo, puedes utilizar Firebase Authentication para el inicio de sesión de usuarios o Firebase Cloud Firestore para almacenar datos en la base de datos.

```jsx
import React, { useState } from 'react';
import { View, Text, Button } from 'react-native';
import auth from '@react-native-firebase/auth';

const HomeScreen = () => {
  const [user, setUser] = useState(null);

  const handleLogout = () => {
    auth()
      .signOut()
      .then(() => {
        console.log('Cierre de sesión exitoso');
      })
      .catch(error => {
        console.log('Error al cerrar sesión:', error.message);
      });
  };

  return (
    <View>
      {user ? (
        <>
          <Text>Bienvenido, {user.email}</Text>
          <Button title="Cerrar Sesión" onPress={handleLogout} />
        </>
      ) : (
        <Text>No has iniciado sesión</Text>
      )}
    </View>
  );
};

export default HomeScreen;
```