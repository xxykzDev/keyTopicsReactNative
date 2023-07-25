# Optimización en React Native

## Resumen: React memo impide la renderizacion de componentes que no recibieron datos nuevos.

## React.memo() => Evitamos renderizaciones innecesarias de componentes funcionales.

### Ejemplo:

Supongamos que tenemos una lista de comentarios, y cada comentario se representa mediante el siguiente componente:

```jsx
import React from 'react';

const Comment = ({ author, content }) => {
  console.log(`Rendering comment from ${author}`);
  
  return (
    <div>
      <p>Author: {author}</p>
      <p>{content}</p>
    </div>
  );
};

export default Comment;
```

Ahora, tenemos un componente padre llamado CommentList que renderiza una lista de comentarios:

```jsx
import React from 'react';
import Comment from './Comment';

const CommentList = ({ comments }) => {
  return (
    <div>
      {comments.map((comment) => (
        <Comment key={comment.id} author={comment.author} content={comment.content} />
      ))}
    </div>
  );
};
export default CommentList;
```

En el ejemplo anterior, cada vez que se produce un cambio en el estado del componente CommentList o cuando se reciben nuevos comentarios desde una API, se volverán a renderizar todos los comentarios, incluso si los datos de los comentarios individuales no han cambiado.

Para evitar renderizaciones innecesarias, podemos utilizar React.memo() en el componente Comment para memorizarlo y evitar su renderización si las props (author y content) no han cambiado. Veamos cómo se hace:

```jsx
import React from 'react';

const Comment = React.memo(({ author, content }) => {
  console.log(`Rendering comment from ${author}`);
  
  return (
    <div>
      <p>Author: {author}</p>
      <p>{content}</p>
    </div>
  );
});

export default Comment;
```

Ahora, cuando utilizamos el componente Comment en CommentList, se beneficiará de la memorización proporcionada por React.memo():

```jsx
import React from 'react';
import Comment from './Comment';

const CommentList = ({ comments }) => {
  return (
    <div>
      {comments.map((comment) => (
        <Comment key={comment.id} author={comment.author} content={comment.content} />
      ))}
    </div>
  );
};

export default CommentList;
```

Gracias a React.memo(), cuando el estado de CommentList cambia o se reciben nuevos comentarios, solo los comentarios con datos actualizados se renderizarán nuevamente, mientras que aquellos con datos inalterados se mantendrán sin cambios. Esto ahorra recursos de renderizado y mejora el rendimiento general de la lista de comentarios.