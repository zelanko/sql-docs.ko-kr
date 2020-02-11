---
title: 명령 준비 및 실행 | Microsoft Docs
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
ms.openlocfilehash: 2295d421f8b802f2f3b531d7de3fc086e43ad572
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924569"
---
# <a name="preparing-and-executing-commands"></a>준비 및 명령 실행
명령은 기본 데이터 원본에 대해 일부 작업을 수행 하기 위해 공급자에 게 실행 되는 명령입니다. 예를 들어 SQL 문은 Microsoft SQL Data Provider에 대 한 명령입니다. ADO에서 명령은 일반적으로 **명령** 개체로 표시 되지만 **연결** 또는 **레코드 집합** 개체를 통해 간단한 명령을 실행할 수도 있습니다.  
  
 **명령** 개체를 사용 하 여 공급자에서 지원 되는 모든 유형의 작업을 요청할 수 있습니다 .이 경우 공급자는 명령 문자열을 올바르게 해석할 수 있습니다. 데이터 공급자에 대 한 일반적인 작업은 데이터베이스를 쿼리하고 레코드를 반환 합니다. **이 개체는** 결과를 저장 하는 컨테이너로 간주할 수 있으며 결과를 볼 수 있는 도구입니다. 많은 ADO 개체와 마찬가지로 일부 **명령** 개체 컬렉션, 메서드 또는 속성은 공급자의 기능에 따라 참조 될 때 오류를 생성할 수 있습니다.  
  
 **명령** 개체를 사용 하는 것 외에도, **연결** 개체에 **Execute** 메서드를 사용 하거나 **레코드 집합** 개체의 **Open** 메서드를 사용 하 여 명령을 실행 하 고 실행 되도록 할 수 있습니다. 그러나 코드에서 명령을 다시 사용 해야 하거나 명령을 사용 하 여 자세한 매개 변수 정보를 전달 해야 하는 경우에는 **command** 개체를 사용 해야 합니다. 이러한 시나리오는이 섹션의 뒷부분에서 자세히 설명 합니다.  
  
> [!NOTE]
>  공급자가 지 원하는 경우 특정 **명령**에서 결과 집합을 이진 스트림 또는 **레코드 집합이**아닌 단일 **레코드로** 반환할 수 있습니다. 또한 일부 **명령은**결과 집합을 반환 하기 위한 것이 아닙니다 (예: SQL Update 쿼리). 이 섹션에서는 가장 일반적인 시나리오를 다룹니다. 그러나 결과를 **레코드 집합** 개체로 반환 하는 **명령을**실행 합니다. 결과를 **레코드나** **스트림으로**반환 하는 방법에 대 한 자세한 내용은 [레코드 및 스트림](../../../ado/guide/data/records-and-streams.md)을 참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [명령 개체 개요](../../../ado/guide/data/command-object-overview.md)  
  
-   [간단한 명령 만들기 및 실행](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [명령 개체 매개 변수](../../../ado/guide/data/command-object-parameters.md)  
  
-   [명령을 사용하여 저장 프로시저 호출](../../../ado/guide/data/calling-a-stored-procedure-with-a-command.md)  
  
-   [연결 개체에서 저장 프로시저를 메서드로 호출](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
-   [명명된 명령](../../../ado/guide/data/named-commands.md)  
  
-   [명명된 명령에 매개 변수 전달](../../../ado/guide/data/passing-parameters-to-a-named-command.md)
