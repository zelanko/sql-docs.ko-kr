---
title: 준비 및 명령 실행 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Command object [ADO], preparing and executing commands
ms.assetid: 7448d9ee-7f4b-47e3-be54-2df8c9bbac32
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6bf2120468a00de2150f6105f4d79ec5a2ed4278
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700460"
---
# <a name="preparing-and-executing-commands"></a>준비 및 명령 실행
명령을 기본 데이터 원본에 대해 일부 작업을 수행 하는 공급자에 실행 하는 명령입니다. SQL 문은 예를 들어 Microsoft SQL 데이터 공급자에 명령입니다. ADO 명령 일반적으로 표시 됩니다 **명령** 개체를 통해 간단한 명령과 발급할 수도 있습니다 하지만 **연결** 하거나 **레코드 집합** 개체입니다.  
  
 사용할 수는 **명령** 공급자 명령 문자열을 올바르게 해석할 수는 가정 하 고 공급자에서 지원 되는 모든 유형의 작업을 요청 하는 개체입니다. 데이터 공급자에 대 한 일반적인 작업은 데이터베이스 쿼리의 레코드를 반환 하는 **레코드 집합** 개체는 결과 및 결과 확인 하는 도구를 저장 하는 컨테이너로 간주할 수 있습니다. ADO 개체와 마찬가지로 일부 **명령** 개체 컬렉션, 메서드 또는 속성 공급자의 기능에 따라 참조 될 때 오류를 생성할 수 있습니다.  
  
 사용 하는 것 외에도 **명령** 개체를 사용할 수는 **Execute** 메서드를 **연결** 개체 또는 **열기** 메서드를  **레코드 집합** 명령을 실행 하는 개체입니다. 하지만 사용 해야를 **명령** 프로그램 명령 사용 하 여 자세한 매개 변수 정보를 전달 해야 하는 경우 코드에서 명령을 다시 사용 하는 경우 또는 개체입니다. 이러한 시나리오는이 섹션의 뒷부분에 자세히 설명 합니다.  
  
> [!NOTE]
>  특정 **명령**결과 이진 스트림으로 또는 단일 집합을 반환할 수 있습니다 **레코드** 아니라는 **레코드 집합**이면이 공급자가 지원 됩니다. 또한 일부 **명령**s 전혀 설정 (예: SQL 업데이트 쿼리) 결과 반환 하지 않습니다. 하지만이 섹션에서는 가장 일반적인 시나리오를 설명: 실행 **명령**결과 반환 하는 **레코드 집합** 개체입니다. 결과를 반환 하는 방법에 대 한 자세한 내용은 **레코드**s 또는 **Stream**를 참조 하십시오 [레코드 및 스트림](../../../ado/guide/data/records-and-streams.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [명령 개체 개요](../../../ado/guide/data/command-object-overview.md)  
  
-   [간단한 명령 만들기 및 실행](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [명령 개체 매개 변수](../../../ado/guide/data/command-object-parameters.md)  
  
-   [명령을 사용하여 저장 프로시저 호출](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [연결 개체의 메서드로 저장된 프로시저를 호출합니다.](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [명명된 명령](../../../ado/guide/data/named-commands.md)  
  
-   [명명된 명령에 매개 변수 전달](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
