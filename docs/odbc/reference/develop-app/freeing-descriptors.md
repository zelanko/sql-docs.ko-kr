---
description: 설명자 해제
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 95c87b7ac70369509a72ff539c63ac888e5f3262
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465805"
---
# <a name="freeing-descriptors"></a>설명자 해제
명시적으로 할당 된 설명자는 연결 핸들이 해제 될 때 SQL_HANDLE_DESC *HandleType* 의 **sqlfreehandle** 을 호출 하 여 명시적으로 해제 하거나 암시적으로 해제할 수 있습니다. 명시적으로 할당 된 설명자가 해제 되 면 해제 된 설명자가 적용 되는 모든 문 핸들은 해당 설명자에 대해 암시적으로 할당 된 설명자로 자동으로 되돌아갑니다.  
  
 암시적으로 할당 된 설명자는 연결에서 열려 있는 문이나 설명자를 삭제 하는 **Sqldisconnect**를 호출 하거나 *HandleType* Of SQL_HANDLE_STMT로 **sqlfreehandle** 을 호출 하 여 문 핸들 및 문과 연결 된 모든 암시적으로 할당 된 설명자를 해제 하는 방법 으로만 해제할 수 있습니다. SQL_HANDLE_DESC *HandleType* 를 사용 하 여 **sqlfreehandle** 을 호출 하 여 암시적으로 할당 된 설명자를 해제할 수 없습니다.  
  
 해제 된 경우에도 암시적으로 할당 된 설명자는 유효한 상태로 유지 되 고 해당 필드에 대해 **SQLGetDescField** 를 호출할 수 있습니다.
