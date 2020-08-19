---
description: 바인딩된 설명자 레코드
title: 바인딩된 설명자 레코드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcf88374967b5a9d8426d16c9e92c06e4eef32cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476805"
---
# <a name="bound-descriptor-records"></a>바인딩된 설명자 레코드
응용 프로그램에서 설명자 레코드의 SQL_DESC_DATA_PTR 필드를 설정 하 여 더 이상 null 값을 포함 하지 않도록 하려면 레코드가 *바인딩되어*있다고 합니다.  
  
 설명자가 APD 인 경우 각 바인딩된 레코드는 바인딩된 매개 변수를 구성 합니다. 입력 매개 변수의 경우 응용 프로그램은 문을 실행 하기 전에 SQL 문의 각 동적 매개 변수 표식에 대 한 매개 변수를 바인딩해야 합니다. 출력 매개 변수의 경우 응용 프로그램에서 매개 변수를 바인딩하지 않아도 됩니다.  
  
 설명자가 데이터베이스 데이터의 행을 설명 하는 인 경우 각 바인딩된 레코드는 바인딩된 열을 구성 합니다.
