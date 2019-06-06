---
title: 결과 받을 | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: edd070cc6f10829b597534d024d767de2a0c7e12
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701712"
---
# <a name="receiving-results"></a>결과 수신
ADO에서 대부분의 명령을 호출자에 게 반환 되는 몇 가지 정보 발생 합니다. 행 집합을 반환 하는 명령에 대 한 결과에서 수신 되는 **레코드 집합** 아마도 가장 사용 되는 ADO 개체의 개체.  
  
 데이터를 수신 하는 방법은 여러 가지는 **레코드 집합** 다음 호출을 포함 하 여 데이터 원본에서 개체:  
  
-   [Connection.Execute 메서드](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Command.Execute 메서드](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Recordset.Open 메서드](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection.NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection.StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 데이터를 받는 **레코드 집합** 개체의 참여를 사용 하 여 데이터를 가져오는 프로세스가 완료 되었으며를 **연결** 개체와 **명령** 개체를 암시적으로 또는 명시적으로 합니다. 일반적인 클라이언트/서버 응용 프로그램 시스템에서 데이터를 가져오는 전체 프로세스가 필요 왕복 네트워크를 통해 각 입력에 대 한 **레코드 집합**합니다.  
  
 에 캡슐화 된 각 데이터 집합에 대 한 네트워크를 통해 몇 가지 확인 해야 하는 방법을 라운드 트립 둘 이상의 결과 집합을 수신 하는 **레코드 집합** 개체입니다. 느리거나 혼잡 네트워크에 대 한 왕복 수가 줄어듭니다 도움이 응용 프로그램의 성능을 개선 합니다. 따라서 일부 공급자 제공 여러 수신 하도록 지원 **레코드 집합**단일 왕복에서. 이 항목에서 설명 되어 있습니다.  
  
-   [다중 레코드 집합 수신](../../../ado/guide/data/receiving-multiple-recordsets.md)
