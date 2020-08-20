---
description: 데이터 가져오기
title: 데이터 가져오기 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, getting data
ms.assetid: 3931e7ec-f66b-4d5d-aad3-c4bf12e8b154
author: rothja
ms.author: jroth
ms.openlocfilehash: c96e12f45a385f34ffe91c1486fd0d63e1be65ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453355"
---
# <a name="getting-data"></a>데이터 가져오기
[Ado 기본 사항](../../../ado/guide/data/ado-fundamentals.md)및 특히 [HelloData](../../../ado/guide/data/hellodata-a-simple-ado-application.md) 예제에는 ado 응용 프로그램 만들기와 관련 된 네 가지 기본 작업 (데이터 가져오기, 데이터 검사, 데이터 편집, 데이터 업데이트)이 도입 되었습니다. 이 섹션에서는 데이터 가져오기에 대해 자세히 설명 합니다.  
  
 기본 수준에서 여러 ADO 개체는 데이터 가져오기 작업에 영향을 주지 않습니다. 먼저 ADO **연결** 개체를 사용 하 여 데이터 원본에 연결 해야 합니다. 그런 다음 ADO **명령** 개체를 사용 하 여 데이터 원본에 명령을 전달 합니다. 마지막으로 대부분의 경우 ADO **레코드 집합** 개체에서 데이터를 수신 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [데이터 원본에 연결](../../../ado/guide/data/connecting-to-data-sources.md)  
  
-   [준비 및 명령 실행](../../../ado/guide/data/preparing-and-executing-commands.md)  
  
-   [결과 수신](../../../ado/guide/data/receiving-results.md)
