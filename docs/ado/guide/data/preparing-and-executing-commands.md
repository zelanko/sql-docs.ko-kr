---
title: 준비 및 실행 명령을 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfe5be8b68fe701d5b44431ab6e10cf8445deda3
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="preparing-and-executing-commands"></a>준비 및 명령 실행
명령은 데이터 원본에 대 한 작업을 수행 하는 공급자에 실행 하는 명령입니다. SQL 문은 예를 들어 Microsoft SQL 데이터 공급자에 명령입니다. ADO, 명령은 일반적으로 표현 된 **명령** 간단한 명령을 통해도 실행할 수 있지만 개체 **연결** 또는 **레코드 집합** 개체입니다.  
  
 사용할 수는 **명령** 공급자 명령 문자열을 올바르게 해석할 수 있는지를 가정 하는 공급자에서 지원 되는 모든 유형의 작업을 요청 하는 개체입니다. 데이터 공급자에 대 한 일반적인 작업은 데이터베이스를 쿼리하고의 레코드를 반환 하는 **레코드 집합** 있는 결과 및 결과 볼 수 있는 도구를 보유 하는 컨테이너로 간주 될 수 있는 개체입니다. ADO 개체와 마찬가지로 일부 **명령** 개체 컬렉션, 메서드 또는 속성 공급자의 기능에 따라 참조 될 때 오류를 생성할 수 있습니다.  
  
 사용 하는 것 외에도 **명령** 개체를 사용할 수 있습니다는 **Execute** 메서드를는 **연결** 개체 또는 **열려** 는 메서드 **레코드 집합** 명령을 실행 하 고 실행 개체입니다. 하지만 사용 해야 한 **명령** 개체 코드에 명령을 다시 사용 하는 경우 또는 사용자의 명령 함께 세부 매개 변수 정보를 전달 하는 경우. 이러한 시나리오는이 섹션의 뒷부분에 자세히 설명 합니다.  
  
> [!NOTE]
>  특정 **명령**결과 집합 또는 단일 이진 스트림으로 반환할 수 있습니다 **레코드** 아니라는 **레코드 집합**,이 공급자가 지원 되는 경우. 또한 일부 **명령**s는 (예: SQL Update 쿼리) 설정 되어 모든 결과 반환할 수 없습니다. 그러나이 섹션은 가장 일반적인 시나리오를 설명: 실행 **명령**로 결과 반환 하는 한 **레코드 집합** 개체입니다. 결과를 반환 하는 방법에 대 한 자세한 내용은 **레코드**s 또는 **스트림**s, 참조 [레코드 및 스트림](../../../ado/guide/data/records-and-streams.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [명령 개체 개요](../../../ado/guide/data/command-object-overview.md)  
  
-   [간단한 명령 만들기 및 실행](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [명령 개체 매개 변수](../../../ado/guide/data/command-object-parameters.md)  
  
-   [명령을 사용하여 저장 프로시저 호출](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [연결 개체의 메서드로 저장된 프로시저를 호출합니다.](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [명명된 명령](../../../ado/guide/data/named-commands.md)  
  
-   [명명된 명령에 매개 변수 전달](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
