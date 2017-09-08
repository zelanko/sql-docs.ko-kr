---
title: "추가 cmdlet은 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 827c8bbc-d48f-4e49-9ea5-abb1380f7623
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e2a71e5b4fb5aae12ce16b419da832d4b1237d28
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="add-rolemember-cmdlet"></a>Add-RoleMember cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Analysis Services 테이블 형식 또는 다차원 데이터베이스의 지정된 역할에 멤버를 추가합니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
## <a name="syntax"></a>구문  
 `Add-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Add-RoleMember [-MemberName] <System.String> [-DatabaseRole] <Microsoft.AnalysisServices.Role> [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Add-RoleMember cmdlet은 유효한 멤버를 기존 데이터베이스 역할에 추가합니다. 데이터베이스 역할만 허용됩니다. 이 cmdlet을 사용하여 멤버를 서버 역할에 추가할 수는 없습니다.  
  
 한 번에 한 멤버만 추가할 있습니다. 이때 멤버는 사용자 또는 그룹 계정일 수 있습니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-membername-string"></a>-MemberName \<문자열 >  
 역할에 추가할 Windows 사용자 또는 그룹을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|0|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-database-string"></a>-데이터베이스 \<문자열 >  
 역할이 속한 데이터베이스를 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|1.|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-rolename-string"></a>-RoleName \<문자열 >  
 멤버를 추가할 역할을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|2|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-databaserole-string"></a>-DatabaseRole \<문자열 >  
 멤버를 추가해야 할 Microsoft.AnalysisServices.Role 개체를 지정합니다. 이 매개 변수는 파이프라인을 통해 데이터베이스 역할을 제공하려는 경우 –Database 및 –RoleName 매개 변수에 대한 대체 항목으로 사용합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|명명됨|  
|기본값||  
|파이프라인 입력 허용|true(ByPropertyName)|  
|와일드카드 문자 허용|false|  
  
### <a name="commonparameters"></a>\<일반 매개 변수 >  
 이 cmdlet은 공통 매개 변수 -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer 및 -OutVariable을 지원합니다. 자세한 내용은 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)를 참조하세요.  
  
## <a name="inputs-and-outputs"></a>입/출력  
 입력 유형은 cmdlet에 파이프할 수 있는 개체 유형입니다. 반환 유형은 cmdlet에서 반환하는 개체 유형입니다.  
  
|||  
|-|-|  
|입력|없음|  
|출력|InclusionThresholdSetting|  
  
## <a name="example-1"></a>예제 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 이 명령은 로컬 기본 인스턴스에서 실행되는 AdventureWorks 데이터베이스에 대해 Windows 도메인 사용자 계정을 Reader 역할에 추가합니다.  
  
## <a name="example-2"></a>예제 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 첫 번째 줄에서는 AWTEST 데이터베이스의 모든 데이터베이스 역할을 파이프라인에 추가합니다. 프롬프트에 $roles를 입력하는 2번 줄에는 역할 배열이 표시됩니다. 3번 줄은 Windows 사용자 adventure-works\bobh를 배열의 첫 번째 역할의 멤버로 추가합니다.  
  
## <a name="example-3"></a>예 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Add-rolemember –membername “adventure-works\bobh”  
```  
  
 이 명령은 Windows 도메인 사용자 계정을 배열의 첫 번째 역할에 추가합니다. 이 배열은 특정 데이터베이스(AWTEST)의 컨텍스트에서 역할 폴더의 자식을 나열하여 만들어집니다.  
  

  
  
