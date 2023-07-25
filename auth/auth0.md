# Auth0

## Crea una cuenta de Auth0: Ve al sitio web de Auth0 (https://auth0.com/) y crea una cuenta utilizando tu correo electrónico y contraseña.

## Crea una aplicación en Auth0: Una vez que hayas iniciado sesión en Auth0, crea una nueva aplicación en la sección "Applications" o "Aplicaciones". Asigna un nombre a tu aplicación y selecciona el tipo de aplicación (por ejemplo, Single Page Application).

## Configura las opciones de autenticación: En la configuración de tu aplicación en Auth0, puedes elegir los proveedores de identidad que desees utilizar, como Google, Facebook, Twitter, etc. También puedes configurar la apariencia y el flujo de inicio de sesión, así como otras opciones de seguridad.

## Obtén las credenciales: Para conectarte con Auth0 en tu aplicación React Native, necesitarás las credenciales de tu aplicación. Ve a la sección "Settings" o "Configuración" de tu aplicación y encontrarás las credenciales necesarias, como el Client ID y el Domain.

# Frontend

## Configuración en la aplicación: En tu archivo App.js (o punto de entrada), importa y configura Auth0 utilizando las credenciales que obtuviste de la plataforma Auth0:

```jsx
import React, { useEffect } from 'react';
import { View, Text, Button } from 'react-native';
import AsyncStorage from '@react-native-community/async-storage';
import { authorize, refresh } from 'react-native-app-auth';

const auth0Config = {
  clientId: 'TU_CLIENT_ID',
  redirectUrl: 'TU_REDIRECT_URL',
  issuer: 'https://TU_AUTH0_DOMAIN',
  scopes: ['openid', 'profile', 'email'],
};

const App = () => {
  const login = async () => {
    try {
      const authState = await authorize(auth0Config);
      // Almacena el token de acceso en AsyncStorage u otra forma de almacenamiento seguro
      await AsyncStorage.setItem('authState', JSON.stringify(authState));
    } catch (error) {
      console.log('Error en el inicio de sesión:', error);
    }
  };

  const logout = async () => {
    // Elimina el token de acceso de AsyncStorage para cerrar la sesión
    await AsyncStorage.removeItem('authState');
  };

  useEffect(() => {
    // Si tienes un token de acceso almacenado, verifica si está vencido y refresca automáticamente
    const checkTokenExpiration = async () => {
      const authState = JSON.parse(await AsyncStorage.getItem('authState'));
      if (authState && authState.accessTokenExpirationDate < new Date().getTime()) {
        try {
          const refreshedState = await refresh(auth0Config, { refreshToken: authState.refreshToken });
          await AsyncStorage.setItem('authState', JSON.stringify(refreshedState));
        } catch (error) {
          console.log('Error al refrescar el token:', error);
        }
      }
    };

    checkTokenExpiration();
  }, []);

  return (
    <View>
      <Text>Bienvenido a mi aplicación</Text>
      <Button title="Iniciar Sesión" onPress={login} />
      <Button title="Cerrar Sesión" onPress={logout} />
    </View>
  );
};

export default App;
```