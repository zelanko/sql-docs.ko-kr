---
title: 커서 라이브러리 운영 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a2297e72aacad7ea91b7af934a47bebbc61f0686
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301620"
---
# <a name="cursor-library-operations"></a>커서 라이브러리 작업
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거됩니다. 새 개발 작업에서 이 기능을 사용하지 말고 현재 이 기능을 사용하는 응용 프로그램을 수정할 계획입니다. 드라이버의 커서 기능을 사용하는 것이 좋습니다.  
  
 ODBC *2.x* 드라이버로 작업하는 응용 프로그램이 ODBC *3.x* 커서 라이브러리를 호출하는 경우 응용 프로그램은 ODBC *2.x* 드라이버에서 지원되지 않는 ODBC *3.x* 기능을 사용할 수 있습니다. 그러나 응용 프로그램 작성기는 이러한 기능을 사용하는 방법을 주의해야 합니다. ODBC *3.x* 커서 라이브러리를 사용하면 ODBC *2.x* 드라이버가 ODBC *3.x* 드라이버로 전환되지 않습니다.
