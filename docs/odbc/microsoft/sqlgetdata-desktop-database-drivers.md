---
title: SQLGetData (데스크톱 데이터베이스 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 086c5381f1801baf919508525c17faab93746ca0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68003362"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData(데스크톱 데이터베이스 드라이버)
이 함수는 바인딩된 열이 있고 열이 검색 되는 순서에 관계 없이 모든 열에서 데이터를 검색할 수 있습니다.  
  
> [!NOTE]  
>  \***SQLGetData** 의 pcbValue는 Jet 4.0 데이터베이스에서 510 자 보다 긴 ANSI 데이터에 바인딩할 때 실제로 사용할 수 있는 것과 동일한 수의 문자를 두 번 반환할 수 있습니다. 510 이하의 문자 값은 실제 cbValue를 반환 합니다.
