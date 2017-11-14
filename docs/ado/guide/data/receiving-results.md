---
title: "결과 수신 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5768404342f76eb8c5999678e6c1a4aa4a3bcd42
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="receiving-results"></a>결과 받기
ADO에서 대부분의 명령을 호출자에 게 반환 하는 몇 가지 정보 발생 합니다. 행 집합을 반환 하는 명령에 대 한 결과에서 수신 되는 **레코드 집합** 개체 수는 가장 많이 사용 되는 ADO 개체입니다.  
  
 여러 가지 방법으로 데이터를 받을 수는 **레코드 집합** 다음 호출 하는 등 데이터 원본의 개체:  
  
-   [Connection.Execute 메서드](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command.Execute 메서드](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Recordset.Open 메서드](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection.NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection.StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 데이터 받기는 **레코드 집합** 개체의 참여를 사용 하 여 데이터를 가져오는 과정을 완료 한 **연결** 개체 및 **명령** 개체를 암시적으로 또는 명시적으로 합니다. 일반적인 클라이언트/서버 응용 프로그램 시스템의 데이터를 가져오는 전체 과정을 사용 하려면 왕복 네트워크를 통해 for 채워진 각 **레코드 집합**합니다.  
  
 에 캡슐화 된 각 데이터 집합에 대 한 네트워크를 통해 여러 해야 하는 수단 라운드 트립 둘 이상의 결과 집합을 받을 수는 **레코드 집합** 개체입니다. 느리거나 혼잡 한 네트워크에 대 한 왕복 수를 줄이고 성능을 높일 수 있습니다는 응용 프로그램의 성능입니다. 일부 공급자의 여러 받으려는 지원 제공 따라서 **레코드 집합**s 단일 왕복에서 합니다. 다음 항목에 설명 되어 있음:  
  
-   [다중 레코드 집합 수신](../../../ado/guide/data/receiving-multiple-recordsets.md)

