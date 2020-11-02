---
description: MSSQLSERVER_17112
title: MSSQLSERVER_17112
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17112 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 870f9b9f4d3fcc8186ed1d16faee861ed63e4135
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418801"
---
# <a name="mssqlserver_17112"></a>MSSQLSERVER_17112
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>세부 정보

|attribute|값|
|---|---|
|제품 이름|SQL Server|
|이벤트 ID|17112|
|이벤트 원본|MSSQLSERVER|
|구성 요소|SQLEngine|
|심볼 이름|INIT_INVCOMMAND|
|메시지 텍스트|잘못된 시작 옵션 a가 레지스트리 또는 명령 프롬프트에서 지정되었습니다. 옵션을 수정하거나 제거하십시오.|
||

## <a name="explanation"></a>설명

이 오류는 잘못된 [데이터베이스 엔진 서비스 시작 옵션](/sql/database-engine/configure-windows/database-engine-service-startup-options)이 지정되었음을 나타냅니다. 시작 옵션을 제대로 지정하지 않으면 SQL Server가 시작되지 않거나 예상대로 실행되지 않을 수 있습니다. 오류 17112도 발생합니다.

인스턴스가 시작되는 경우도 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그를 검토하면 시작 매개 변수가 다음과 같이 올바르게 표시되지 않습니다.

> \<Datetime> 서버 레지스트리 시작 매개 변수:  
\<Datetime> 서버 -d D:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\DATA\master.mdf  
\<Datetime> 서버 -e D:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\LOG\ERRORLOG  
\<Datetime> 서버 -l D:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\DATA\mastlog.ldf  
\<Datetime> 서버 -T1118 -g512

마지막 두 개의 시작 매개 변수가 동일한 줄에 어떻게 표시되는지 확인합니다.

필요한 시작 매개 변수를 추가해도 서버 동작에 의도한 효과가 나타나지 않는 경우도 있습니다.

## <a name="possible-causes"></a>가능한 원인

이 문제는 다음과 같은 이유로 인해 발생합니다.

- 유효한 시작 매개 변수 목록에 없는 시작 매개 변수 사용
- 적절한 구분 기호[;] 없이 시작 매개 변수 지정
- 텍스트 편집기에서 시작 매개 변수를 복사하여 붙여넣는 동안 표시되지 않는 특수 문자 추가(예: -T 앞에 공백 추가)
- 시작 매개 변수에 올바른 대/소문자 사용 안 함

## <a name="user-action"></a>사용자 조치

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager 도구를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대해 시작 매개 변수를 지정하고 유효성을 검사합니다. 각 시작 매개 변수를 적절하게 구분하고 특수 문자가 포함되지 않도록 합니다.

## <a name="more-information"></a>자세한 정보

본 문서에 대한 자세한 내용은 다음 문서를 참조하세요.

- [데이터베이스 엔진 서비스 시작 옵션](/sql/database-engine/configure-windows/database-engine-service-startup-options)
- [SCM 서비스 - 서버 시작 옵션 구성](/sql/database-engine/configure-windows/scm-services-configure-server-startup-options)
