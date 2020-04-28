---
title: 결과 받기 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b861553e9a71ce56377f8d87bba0f9e26e929c2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924521"
---
# <a name="receiving-results"></a>결과 수신
ADO에서 대부분의 명령은 호출자에 게 일부 정보를 반환 합니다. 행 집합을 반환 하는 명령의 경우 결과는 ADO 개체에서 가장 많이 사용 되는 **레코드 집합** 개체로 수신 됩니다.  
  
 다음을 호출 하는 등의 여러 가지 방법으로 데이터 원본에서 **레코드 집합** 개체의 데이터를 받을 수 있습니다.  
  
-   [Connection Execute 메서드](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command Execute 메서드](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Recordset. Open 메서드](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection. NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [연결. StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 **레코드 집합** 개체에서 데이터를 받으면 **연결** 개체 및 **명령** 개체의 참여를 암시적으로 또는 명시적으로 하 여 데이터를 가져오는 프로세스를 마칩니다. 일반적인 클라이언트/서버 응용 프로그램 시스템에서 데이터를 가져오는 전체 프로세스에는 채워진 각 **레코드 집합**에 대해 네트워크를 통해 라운드트립이 필요 합니다.  
  
 결과 집합을 두 개 이상 수신 하려면 네트워크를 통해 여러 번 왕복 해야 합니다. 즉, **레코드** 집합 개체에 캡슐화 된 각 데이터 집합에 대해 하나씩 수행 해야 합니다. 네트워크 속도가 느리거나 혼잡 한 경우 왕복 횟수를 줄이면 응용 프로그램의 성능 향상에 도움이 될 수 있습니다. 따라서 일부 공급자는 단일 왕복에서 여러 **레코드 집합**을 받을 수 있는 지원을 제공 합니다. 이에 대해서는 다음 항목에서 설명 합니다.  
  
-   [다중 레코드 집합 수신](../../../ado/guide/data/receiving-multiple-recordsets.md)
