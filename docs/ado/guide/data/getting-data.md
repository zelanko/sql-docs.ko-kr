---
description: 데이터 가져오기
title: 데이터 가져오기 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, getting data
ms.assetid: 3931e7ec-f66b-4d5d-aad3-c4bf12e8b154
author: rothja
ms.author: jroth
ms.openlocfilehash: 3223d2291ba15ab0a2c14b1fac2aaea911bde395
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980774"
---
# <a name="getting-data"></a>데이터 가져오기
[Ado 기본 사항](./ado-fundamentals.md)및 특히 [HelloData](./hellodata-a-simple-ado-application.md) 예제에는 ado 응용 프로그램 만들기와 관련 된 네 가지 기본 작업 (데이터 가져오기, 데이터 검사, 데이터 편집, 데이터 업데이트)이 도입 되었습니다. 이 섹션에서는 데이터 가져오기에 대해 자세히 설명 합니다.  
  
 기본 수준에서 여러 ADO 개체는 데이터 가져오기 작업에 영향을 주지 않습니다. 먼저 ADO **연결** 개체를 사용 하 여 데이터 원본에 연결 해야 합니다. 그런 다음 ADO **명령** 개체를 사용 하 여 데이터 원본에 명령을 전달 합니다. 마지막으로 대부분의 경우 ADO **레코드 집합** 개체에서 데이터를 수신 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [데이터 원본에 연결](./connecting-to-data-sources.md)  
  
-   [준비 및 명령 실행](./preparing-and-executing-commands.md)  
  
-   [결과 수신](./receiving-results.md)