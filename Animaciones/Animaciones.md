# Animated API

# Resumen: utilizamos Animated API porque se ejecutan en un hilo separado al de la UI (otro threa o hilo de js) de la app, y esto permite la fluidez de las mismas sin bloquear el flujo de nuestra app o utilizar recursos usados por el hilo de UI

## Rste API te permite animar directamente las propiedades de estilo de tus componentes, como posición, tamaño, opacidad y rotación, utilizando el hilo de JavaScript para manejar las animaciones sin afectar el rendimiento del hilo principal.

## El Animated API es una parte integral de React Native y está diseñado para ofrecer un rendimiento óptimo en dispositivos móviles. Al utilizar Animated, las animaciones se ejecutan en el hilo de JavaScript, lo que permite que el hilo principal se mantenga receptivo y sin bloqueos mientras se realizan las animaciones. Además, Animated aprovecha las capacidades de animación nativa de las plataformas (iOS y Android), lo que resulta en animaciones fluidas y con una apariencia nativa en ambas plataformas.

## Implementacion ejemplo

```jsx

import React, { useEffect, useRef } from 'react';
import { Animated, View, Text, Button } from 'react-native';

const FadeAnimation = () => {
  const fadeValue = useRef(new Animated.Value(0)).current;

  const startAnimation = () => {
    Animated.timing(fadeValue, {
      toValue: 1,
      duration: 1000,
      useNativeDriver: true,
    }).start();
  };

  useEffect(() => {
    startAnimation();
  }, []);

  return (
    <View>
      <Animated.View style={{ opacity: fadeValue }}>
        <Text>Fade In Animation</Text>
      </Animated.View>
    </View>
  );
};

export default FadeAnimation;
```

## En este ejemplo, se utiliza Animated.timing() para crear una animación de desvanecimiento del texto. La propiedad opacity del componente Animated.View se anima desde un valor inicial de 0 (invisible) a un valor final de 1 (completamente visible) durante una duración de 1000 milisegundos. Al usar useNativeDriver: true, la animación se ejecutará de manera nativa en el dispositivo, lo que garantiza un rendimiento óptimo.
