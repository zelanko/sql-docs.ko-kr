---
title: Remove-rolemember cmdlet | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e38f56ab-facd-4bef-9502-f52f8486a6a6
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ad8117fd1b8c936914291484d7dde26702e119a1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="remove-rolemember-cmdlet"></a>Remove-RoleMember cmdlet
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Analysis Services 데이터베이스의 지정된 된 역할에서 구성원을 제거 합니다.  

>[!NOTE] 
>이 문서는 오래 된 내용 및 예제에 포함 될 수 있습니다. 최신에 대 한 Get-help cmdlet을 사용 합니다.
  
## <a name="syntax"></a>구문  
 `Remove-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Remove-RoleMember [-DatabaseRole] <Microsoft.AnalysisServices.Role> [-MemberName] <System.String>  [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Remove-RoleMember cmdlet은 Analysis Services 데이터베이스의 역할에서 기존 멤버를 제거합니다.  
  
## <a name="parameters"></a>매개 변수  
  
### <a name="-membername-string"></a>-MemberName \<문자열 >  
 역할에서 제거할 Windows 사용자 또는 그룹을 지정합니다.  
  
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
|위치|1|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-rolename-string"></a>-RoleName \<문자열 >  
 멤버를 제거하려는 역할을 지정합니다.  
  
|||  
|-|-|  
|필수 여부|true|  
|위치|2|  
|기본값||  
|파이프라인 입력 허용|false|  
|와일드카드 문자 허용|false|  
  
### <a name="-databaserole-string"></a>-DatabaseRole \<문자열 >  
 멤버를 제거하려는 Microsoft.AnalysisServices.Role 개체를 지정합니다. 이 매개 변수는 파이프라인을 통해 데이터베이스 역할을 제공하려는 경우 –Database 및 –RoleName 매개 변수에 대한 대체 항목으로 사용합니다.  
  
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
 없음  
  
## <a name="example-1"></a>예 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 이 명령은 로컬 기본 인스턴스에서 실행 중인 AdventureWorks 데이터베이스에 대해 읽기 역할에서 Windows 도메인 사용자 계정을 제거합니다.  
  
## <a name="example-2"></a>예 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 첫 번째 줄에서는 AWTEST 데이터베이스의 모든 데이터베이스 역할을 파이프라인에 추가합니다. 프롬프트에 $roles를 입력하는 2번 줄에는 역할 배열이 표시됩니다. 3번 줄은 배열의 첫 번째 역할에서 Windows 사용자 “adventure-works\bobh”를 제거합니다.  
  
## <a name="example-3"></a>예제 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Remove-rolemember –membername “adventure-works\bobh”  
```  
  
 이 명령은 특정 데이터베이스(AWTEST)의 컨텍스트에서 역할 폴더의 자식을 나열하여 만든 배열의 첫 번째 역할에서 Windows 도메인 사용자 계정을 제거합니다.  
  

  
  
