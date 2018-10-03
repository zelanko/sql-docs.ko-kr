---
title: 설명자 해제 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d643ccad0110796127524a10e82aef7c3339b163
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694632"
---
# <a name="freeing-descriptors"></a>설명자 해제
명시적으로 할당 된 설명자 수 중 하나를 명시적으로 호출 하 여 해제할 **SQLFreeHandle** 사용 하 여 *HandleType* SQL_HANDLE_DESC, 또는 암시적으로 때 연결 핸들을 해제 됩니다. 명시적으로 할당 된 설명자를 해제 하는 경우, 모든 문 핸들을 자동으로 적용 해제 된 설명자에 암시적으로 할당 된 설명자를 되돌립니다.  
  
 만 호출 하 여 암시적으로 할당 된 설명자를 해제할 수 있습니다 **SQLDisconnect**를 삭제 하는 모든 문 또는 설명자에 연결 하거나 호출 하 여 엽니다 **SQLFreeHandle** 사용 하 여는  *HandleType* 무료 문 핸들 및 문과 연결 된 모든 암시적으로 할당 된 설명자를 호출 하 여입니다. 암시적으로 할당 된 설명자를 호출 하 여 해제할 수 없습니다 **SQLFreeHandle** 사용 하 여를 *HandleType* SQL_HANDLE_DESC입니다.  
  
 암시적으로 할당 된 설명자를 계속 유효 하며 해제 하는 경우에 하 고 **SQLGetDescField** 해당 필드에 호출할 수 있습니다.
