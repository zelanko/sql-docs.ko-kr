---
title: 설명자 확보 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c96d5b654d8331f95e3abbe8a3aa8b563bf7a63
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911578"
---
# <a name="freeing-descriptors"></a>설명자를 해제합니다.
명시적으로 할당 된 설명자 될 수 있습니다 하나를 명시적으로 호출 하 여 해제 **SQLFreeHandle** 와 *HandleType* SQL_HANDLE_DESC, 또는 암시적으로 때 연결 핸들 해제 됩니다. 명시적으로 할당 된 설명자는 해제, 모든 문 핸들을 자동으로 적용 해제 된 설명자에 암시적으로 할당 된 설명자를 되돌립니다.  
  
 암시적으로 할당 된 설명자만 호출 하 여 해제할 수 있도록 **SQLDisconnect**하거나, 모든 문을 삭제 하는 설명자 열에 연결 하거나 호출 하 여 **SQLFreeHandle** 와  *HandleType* 여 문 핸들을 문과 연결 된 모든 암시적으로 할당 된 설명자를입니다. 암시적으로 할당 된 설명자를 호출 하 여 해제할 수 없습니다 **SQLFreeHandle** 와 *HandleType* SQL_HANDLE_DESC입니다.  
  
 해제 하는 경우에 암시적으로 할당 된 설명자 계속 유효 하 고 **SQLGetDescField** 해당 필드에 호출할 수 있습니다.
