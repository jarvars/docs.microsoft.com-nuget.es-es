---
title: Plantilla de URL de detalles de paquete, API de NuGet
description: La plantilla de dirección URL de detalles del paquete permite a los clientes Mostrar en su interfaz de usuario un vínculo Web a más detalles del paquete.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 1b84c6e88a56216e5747d5bc602219af6695c305
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2020
ms.locfileid: "76812940"
---
# <a name="package-details-url-template"></a>Plantilla de URL de detalles de paquete

Un cliente puede crear una dirección URL que el usuario pueda usar para ver más detalles del paquete en su explorador Web. Esto resulta útil cuando un origen de paquete desea mostrar información adicional sobre un paquete que puede no ajustarse dentro del ámbito de lo que muestra la aplicación cliente de NuGet.

El recurso usado para generar esta dirección URL es el `PackageDetailsUriTemplate` recurso que se encuentra en el [Índice de servicio](service-index.md).

## <a name="versioning"></a>Control de versiones

Se usan los siguientes valores de `@type`:

Valor de @type                     | Notas
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | La versión inicial

## <a name="url-template"></a>Plantilla de dirección URL

La dirección URL de la siguiente API es el valor de la propiedad `@id` asociada a uno de los valores de `@type` de recursos mencionados anteriormente.

## <a name="http-methods"></a>Métodos HTTP

Aunque el cliente no está diseñado para realizar solicitudes a la dirección URL del paquete de detalles en nombre del usuario, la página web debe admitir el método `GET` para permitir que se pueda abrir fácilmente una dirección URL en un explorador Web.

## <a name="construct-the-url"></a>Construir la dirección URL

Dado un identificador de paquete conocido y una versión, la implementación del cliente puede construir una dirección URL que se usa para tener acceso a una interfaz Web. La implementación del cliente debe mostrar esta dirección URL construida (o vínculo en el que se pueda hacer clic) al usuario, lo que le permite abrir un explorador Web en la dirección URL y obtener más información sobre el paquete. El contenido de la página de detalles del paquete viene determinado por la implementación del servidor.

La dirección URL debe ser una dirección URL absoluta y el esquema (Protocolo) debe ser HTTPS.

El valor de la `@id` en el índice de servicio es una cadena de dirección URL que contiene cualquiera de los siguientes tokens de marcador de posición:

### <a name="url-placeholders"></a>Marcadores de posición de dirección URL

Name        | Tipo de    | Requerido | Notas
----------- | ------- | -------- | -----
`{id}`      | cadena  | No       | Identificador del paquete para el que se van a obtener detalles.
`{version}` | cadena  | No       | La versión del paquete para obtener detalles

El servidor debe aceptar los valores `{id}` y `{version}` con cualquier grafía. Además, el servidor no debe ser sensible a si la versión está [normalizada](../concepts/package-versioning.md#normalized-version-numbers). En otras palabras, el servidor debe aceptar también aceptar versiones no normalizadas.

Por ejemplo, la plantilla de detalles del paquete de Nuget. org tiene el siguiente aspecto:

    https://www.nuget.org/packages/{id}/{version}

Si la implementación del cliente necesita mostrar un vínculo a los detalles del paquete de NuGet. control de versiones 4.3.0, generaría la siguiente dirección URL y la proporcionará al usuario:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
