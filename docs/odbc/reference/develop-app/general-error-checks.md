---
title: 일반 오류 검사 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- general error checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0c9a3425-0a7c-48de-9ff6-73601c26283e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 35dc509e0bda51c8d219b76f48b44b2b03dba8cc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305564"
---
# <a name="general-error-checks"></a>일반 오류 검사
드라이버 관리자는 한 가지 일반적인 오류를 확인 합니다. 다음 오류가 발생할 경우 항상 SQL_ERROR을 반환 합니다. 함수는 드라이버에서 지원 되어야 합니다.
