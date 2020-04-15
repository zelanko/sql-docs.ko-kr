---
title: 설명자 해방 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af30ceb29e032764b89aa2069086aa898a7d35db
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305604"
---
# <a name="freeing-descriptors"></a>설명자 해제
명시적으로 할당된 설명자는 handleType SQL_HANDLE_DESC *handleType을* 사용하는 **SQLFreeHandle을** 호출하거나 연결 핸들이 해제될 때 암시적으로 해제될 수 있습니다. 명시적으로 할당된 설명자가 해제되면 해제된 설명자가 적용된 모든 문이 암시적으로 할당된 설명자로 자동으로 되돌아갑니다.  
  
 암시적으로 할당된 설명자는 연결에서 열리는 모든 문이나 설명기를 삭제하는 **SQLDisconnect를**호출하거나 문 핸들과 문과 연결된 모든 암시적으로 할당된 설명기를 해제하기 위해 *handleType* SQL_HANDLE_STMT **SQLFreeHandle을** 호출하여 해제할 수 있습니다. 암시적으로 할당된 설명자는 *핸들 유형* SQL_HANDLE_DESC **SQLFreeHandle을** 호출하여 해제할 수 없습니다.  
  
 해제된 경우에도 암시적으로 할당된 설명자는 유효하며 **SQLGetDescField는** 해당 필드에서 호출할 수 있습니다.
