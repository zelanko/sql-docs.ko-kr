---
title: ALTER ASSEMBLY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ASSEMBLY_TSQL
- ALTER ASSEMBLY
dev_langs: TSQL
helpviewer_keywords:
- assemblies [CLR integration], modifying
- refreshing assemblies
- assemblies [CLR integration], versioning
- assemblies [CLR integration], adding files
- modifying assemblies
- adding files
- ALTER ASSEMBLY statement
ms.assetid: 87bca678-4e79-40e1-bb8b-bd5ed8f34853
caps.latest.revision: "76"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8b8918d653d6d9ff5f26588ad1626bfc62e3679d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="alter-assembly-transact-sql"></a>ALTER ASSEMBLY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  어셈블리의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 카탈로그 속성을 수정하여 어셈블리를 변경합니다. ALTER ASSEMBLY를 새로 고치고 어셈블리의 최신 복사본으로는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 의 구현을 유지 하 고 추가 하거나 연관 된 파일을 제거 하는 모듈입니다. 어셈블리를 사용 하 여 만들어진 [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md)합니다.  

>  [!WARNING]
>  CLR은 더 이상 보안 경계로 지원되지 않는 .NET Framework의 CAS(코드 액세스 보안)를 사용합니다. `PERMISSION_SET = SAFE`로 만든 CLR 어셈블리에서 외부 시스템 리소스에 액세스하고, 비관리 코드를 호출하고, sysadmin 권한을 얻을 수 있습니다. [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]부터 CLR 어셈블리의 보안을 강화하기 위해 `clr strict security`라는 `sp_configure` 옵션이 도입되었습니다. `clr strict security`는 기본적으로 사용되며 `SAFE` 및 `EXTERNAL_ACCESS` 어셈블리가 `UNSAFE`로 표시된 것처럼 처리됩니다. `clr strict security` 옵션은 이전 버전과의 호환성을 위해 사용하지 않도록 설정할 수 있지만 권장하지는 않습니다. 모든 어셈블리는 master 데이터베이스에서 `UNSAFE ASSEMBLY` 권한이 부여된 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명하는 것이 좋습니다. 자세한 내용은 [CLR strict security](../../database-engine/configure-windows/clr-strict-security.md)를 참조하세요.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
ALTER ASSEMBLY assembly_name  
    [ FROM <client_assembly_specifier> | <assembly_bits> ]  
    [ WITH <assembly_option> [ ,...n ] ]  
    [ DROP FILE { file_name [ ,...n ] | ALL } ]  
    [ ADD FILE FROM   
    {   
        client_file_specifier [ AS file_name ]   
      | file_bits AS file_name   
    } [,...n ]   
    ] [ ; ]  
<client_assembly_specifier> :: =  
    '\\computer_name\share-name\[path\]manifest_file_name'  
  | '[local_path\]manifest_file_name'  
  
<assembly_bits> :: =  
    { varbinary_literal | varbinary_expression }  
  
<assembly_option> :: =  
    PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE }   
  | VISIBILITY = { ON | OFF }  
  | UNCHECKED DATA  
  
```  
  
## <a name="arguments"></a>인수  
 *assembly_name*  
 수정하려는 어셈블리의 이름입니다. *assembly_name* 데이터베이스에 이미 있어야 합니다.  
  
 FROM \<client_assembly_specifier> | \<assembly_bits>  
 어셈블리의 구현을 유지하는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 모듈의 최신 복사본으로 어셈블리를 업데이트합니다. 지정한 어셈블리와 관련된 파일이 없는 경우에만 이 옵션을 사용할 수 있습니다.  
  
 \<client_assembly_specifier > 네트워크 또는 새로 고칠 어셈블리가 있는 로컬 위치를 지정 합니다. 네트워크 위치에는 컴퓨터 이름, 공유 이름 및 해당 공유 내의 경로가 포함됩니다. *manifest_file_name* 어셈블리의 매니페스트가 포함 된 파일의 이름을 지정 합니다.  
  
 \<assembly_bits > 어셈블리에 대 한 이진 값입니다.  
  
 업데이트도 필요한 모든 종속 어셈블리에 대해 별도의 ALTER ASSEMBLY 문을 실행해야 합니다.  
  
 PERMISSION_SET = { SAFE | EXTERNAL_ACCESS | UNSAFE }   
>  [!IMPORTANT]  
>  `PERMISSION_SET` 옵션에 영향을 받는 `clr strict security` 열기 경고에 설명 된 옵션입니다. 때 `clr strict security` 가 사용 하도록 설정으로 모든 어셈블리로 처리 `UNSAFE`합니다.  
 어셈블리의 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 코드 액세스 권한 설정 속성을 지정합니다. 이 속성에 대 한 자세한 내용은 참조 하세요. [CREATE assembly&#40; Transact SQL &#41; ](../../t-sql/statements/create-assembly-transact-sql.md).  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 EXTERNAL_ACCESS 및 UNSAFE 옵션을 사용할 수 없습니다.  
  
 VISIBILITY = { ON | OFF }  
 어셈블리에 대해 CLR(공용 언어 런타임) 함수, 저장 프로시저, 트리거, 사용자 정의 형식 및 사용자 정의 집계 함수를 만들 때 어셈블리를 표시할지 여부를 나타냅니다. 이 인수가 OFF로 설정되어 있으면 어셈블리가 다른 어셈블리에서 호출되는 용도로만 사용됩니다. 어셈블리에 대해 생성된 기존 CLR 데이터베이스가 있는 경우 어셈블리의 표시 유형을 변경할 수 없습니다. 참조 하는 모든 어셈블리 *assembly_name* 기본적으로 표시 되지 않는 상태로 업로드 됩니다.  
  
 UNCHECKED DATA  
 기본적으로 개별 테이블 행의 일관성을 확인해야 하는 경우 ALTER ASSEMBLY가 실패합니다. 이 옵션을 사용하면 나중에 DBCC CHECKTABLE을 사용할 때까지 일관성 확인을 연기할 수 있습니다. 이 옵션을 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 데이터베이스에 다음을 포함하는 테이블이 있는 경우에도 ALTER ASSEMBLY 문을 실행합니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 함수나 메서드를 통해 직접 또는 간접적으로 어셈블리의 메서드를 참조하는 지속형 계산 열  
  
-   직접 또는 간접적으로 어셈블리의 메서드를 참조하는 CHECK 제약 조건  
  
-   구성 요소의 어셈블리 및 형식 구현에 종속 된 CLR 사용자 정의 형식의 열을 **UserDefined** (비-**네이티브**) serialization 형식입니다.  
  
-   WITH SCHEMABINDING을 사용하여 생성된 뷰를 참조하는 CLR 사용자 정의 형식의 열  
  
 CHECK 제약 조건이 있는 경우 비활성화되며 신뢰할 수 없는 상태로 표시됩니다. 어셈블리에 의존하는 열이 포함된 모든 테이블은 명시적으로 확인되기 전까지 확인되지 않은 데이터를 포함하는 것으로 표시됩니다.  
  
 구성원만는 **db_owner** 및 **db_ddlowner** 고정된 데이터베이스 역할이이 옵션을 지정할 수 있습니다.  
  
 필요는 **ALTER ANY SCHEMA** 이 옵션을 지정할 수 있는 권한이 있습니다.  
  
 자세한 내용은 참조 [구현 어셈블리](../../relational-databases/clr-integration/assemblies-implementing.md)합니다.  
  
 [ DROP FILE { *file_name*[ **,***...n*] | ALL } ]  
 어셈블리와 관련된 특정 파일이나 모든 파일을 데이터베이스에서 제거합니다. ADD FILE이 뒤따를 경우 DROP FILE이 먼저 실행됩니다. 이 기능을 사용하여 같은 파일 이름의 파일을 대체할 수 있습니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
 [ADD FILE FROM { *client_file_specifier* [AS *file_name*] | *file_bits*AS *file_name*}  
 소스 코드와 같은 어셈블리와 연결할 파일을 업로드 디버그 파일 또는 기타 관련 정보를 서버에 표시 될 수는 **sys.assembly_files** 카탈로그 뷰에 있습니다. *client_file_specifier* 에서 파일을 업로드 하는 위치를 지정 합니다. *file_bits* 파일 구성 하는 이진 값의 목록을 지정 하려면 대신 사용할 수 있습니다. *file_name* 는 파일에에서 저장할지 인스턴스의 이름을 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. *file_name* 지정 하지 않은 경우 *file_bits* 지정 하는 선택 사항 경우 *client_file_specifier* 지정 됩니다. 경우 *file_name* 를 지정 하지 않으면의 file_name 부분이 *client_file_specifier* 으로 사용 됩니다 *file_name*합니다.  
  
> [!NOTE]  
>  포함된 데이터베이스에서는 이 옵션을 사용할 수 없습니다.  
  
## <a name="remarks"></a>주의  
 ALTER ASSEMBLY는 현재 실행 중인 세션(수정 중인 어셈블리에서 실행 중인 코드)을 방해하지 않습니다. 현재 세션은 어셈블리의 변경되지 않은 비트를 사용하여 실행이 완료됩니다.  
  
 FROM 절이 지정되면 ALTER ASSEMBLY는 제공된 모듈의 최신 복사본을 기준으로 어셈블리를 업데이트합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 어셈블리에 대해 정의된 CLR 함수, 저장 프로시저, 트리거, 데이터 형식 및 사용자 정의 집계 함수가 있을 수 있으므로 ALTER ASSEMBLY 문은 이러한 항목을 어셈블리의 최신 구현에 다시 바인딩합니다. 이렇게 다시 바인딩하기 위해서는 동일한 서명의 수정된 어셈블리에도 CLR 함수, 저장 프로시저 및 트리거를 매핑하는 메서드가 있어야 합니다. CLR 사용자 정의 형식 및 사용자 정의 집계 함수를 구현하는 클래스는 여전히 사용자 정의 형식이나 집계에 대한 요구 사항을 충족해야 합니다.  
  
> [!CAUTION]  
>  WITH UNCHECKED DATA를 지정하지 않으면 새 어셈블리 버전이 테이블, 인덱스 또는 다른 영구 사이트의 기존 데이터에 영향을 주는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 ALTER ASSEMBLY를 실행하지 못하도록 합니다. 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 CLR 어셈블리를 업데이트할 때 계산 열, 인덱스, 인덱싱된 뷰 또는 식이 기본 루틴 및 유형과 일치하도록 보장하지는 않습니다. ALTER ASSEMBLY를 실행하여 어셈블리에 저장된 해당 식을 기반으로 하는 식 결과와 값이 일치하는지 확인하는 경우 주의하십시오.  
  
 ALTER ASSEMBLY는 어셈블리 버전을 변경합니다. 어셈블리의 culture 및 공개 키 토큰은 동일하게 유지됩니다.  
  
 다음을 변경하는 데 ALTER ASSEMBLY 문을 사용할 수 없습니다.  
  
-   어셈블리를 참조하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 CLR 함수, 집계 함수, 저장 프로시저 및 트리거의 서명. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 어셈블리의 새 버전으로 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 개체를 다시 바인딩할 수 없는 경우 ALTER ASSEMBLY가 실패합니다.  
  
-   다른 어셈블리에서 호출되는 어셈블리에 있는 메서드의 서명  
  
-   참조 되는 어셈블리에 종속 된 어셈블리 목록에서 **DependentList** 해당 어셈블리의 속성입니다.  
  
-   해당 메서드에 직접 또는 간접적으로 의존하는 인덱스나 지속형 계산 열이 없는 경우 메서드의 인덱싱 가능성  
  
-   **FillRow** CLR 테이블 반환 함수에 대 한 메서드 이름 특성입니다.  
  
-   **Accumulate** 및 **Terminate** 사용자 정의 집계에 대 한 메서드 서명을 합니다.  
  
-   시스템 어셈블리  
  
-   어셈블리 소유권. 사용 하 여 [ALTER authorization&#40; Transact SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md) 대신 합니다.  
  
 또한 사용자 정의 형식을 구현하는 어셈블리에 대해 다음 변경을 수행하는 경우에만 ALTER ASSEMBLY를 사용할 수 있습니다.  
  
-   서명 또는 특성이 변경되지 않는 경우 사용자 정의 형식 클래스의 공용 메서드를 수정하는 경우  
  
-   새 공용 메서드를 추가하는 경우  
  
-   전용 메서드를 어떤 방식으로든 수정하는 경우  
  
 데이터 멤버 또는 기본 클래스를 비롯하여 기본적으로 직렬화된 사용자 정의 형식에 포함된 필드는 ALTER ASSEMBLY를 사용하여 변경할 수 없습니다. 다른 모든 변경은 지원되지 않습니다.  
  
 ADD FILE FROM을 지정하지 않을 경우 ALTER ASSEMBLY는 어셈블리와 관련된 모든 파일을 삭제합니다.  
  
 UNCHECKED 데이터 절 없이 ALTER ASSEMBLY를 실행하면 새 어셈블리 버전이 테이블의 기존 데이터에 영향을 미치지 않는지 확인하는 검사가 수행됩니다. 확인해야 하는 데이터 양에 따라 이 검사가 성능에 영향을 미칠 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 어셈블리에 대한 ALTER 권한이 필요합니다. 추가 요구 사항은 다음과 같습니다.  
  
-   기존 사용 권한을 가진 어셈블리를 변경 하려면 집합은 EXTERNAL_ACCESS, 필요**EXTERNAL ACCESS ASSEMBLY**서버에 대 한 권한이 있습니다.  
  
-   설정 되어 안전 하지 않은 기존 사용 권한을 가진 어셈블리를 변경 하려면 필요 **UNSAFE ASSEMBLY** 서버에 대 한 권한이 있습니다.  
  
-   External_access로 어셈블리의 권한 집합을 변경 하려면**EXTERNAL ACCESS ASSEMBLY** 서버에 대 한 권한이 있습니다.  
  
-   UNSAFE를 어셈블리의 권한 집합을 변경 하려면 **UNSAFE ASSEMBLY** 서버에 대 한 권한이 있습니다.  
  
-   검사 되지 않은 데이터를 지정 하면 필요한 **ALTER ANY SCHEMA** 권한.  


### <a name="permissions-with-clr-strict-security"></a>CLR 엄격한 보안 사용 권한    
다음 사용 권한을 CLR 어셈블리를 변경 하기 위해 필요한 경우 `CLR strict security` 사용 됨:

- 사용자에게 `ALTER ASSEMBLY` 권한이 있어야 합니다.  
- 다음 조건 중 하나가 충족되어야 합니다.  
  - 어셈블리는 서버에 대한 `UNSAFE ASSEMBLY` 권한이 있는 해당 로그인이 포함된 인증서 또는 비대칭 키로 서명됩니다. 어셈블리에 서명하는 것이 좋습니다.  
  - 데이터베이스는 `ON`으로 설정된 `TRUSTWORTHY` 속성을 가지고 있고 서버에 대한 `UNSAFE ASSEMBLY` 권한이 있는 로그인으로 소유됩니다. 이 방법은 권장되지 않습니다.  
  
  
 어셈블리 사용 권한 집합에 대 한 자세한 내용은 참조 [어셈블리 디자인](../../relational-databases/clr-integration/assemblies-designing.md)합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-refreshing-an-assembly"></a>1. 어셈블리 새로 고치기  
 다음 예에서는 `ComplexNumber` 어셈블리를 어셈블리의 구현을 유지하는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 모듈의 최신 복사본으로 업데이트합니다.  
  
> [!NOTE]  
>  `ComplexNumber` 어셈블리는 UserDefinedDataType 예제 스크립트를 실행하여 만들 수 있습니다. 자세한 내용은 참조 [사용자 정의 형식](http://msdn.microsoft.com/library/a9b75f36-d7f5-47f7-94d6-b4448c6a2191)합니다.  
  
 ```
 ALTER ASSEMBLY ComplexNumber 
 FROM 'C:\Program Files\Microsoft SQL Server\130\Tools\Samples\1033\Engine\Programmability\CLR\UserDefinedDataType\CS\ComplexNumber\obj\Debug\ComplexNumber.dll' 
  ```
### <a name="b-adding-a-file-to-associate-with-an-assembly"></a>2. 어셈블리와 연결할 파일 추가  
 다음 예에서는 `Class1.cs` 어셈블리와 연결할 소스 코드 파일 `MyClass`를 업로드합니다. 이 예에서는 데이터베이스에 이미 `MyClass` 어셈블리가 있다고 가정합니다.  
  
```  
ALTER ASSEMBLY MyClass   
ADD FILE FROM 'C:\MyClassProject\Class1.cs';  
```  
  
### <a name="c-changing-the-permissions-of-an-assembly"></a>3. 어셈블리의 사용 권한 변경  
 다음 예에서는 `ComplexNumber` 어셈블리 사용 권한 설정을 SAFE에서 `EXTERNAL ACCESS`로 변경합니다.  
  
```  
ALTER ASSEMBLY ComplexNumber WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [어셈블리 &#40; 만들기 Transact SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [DROP assembly&#40; Transact SQL &#41;](../../t-sql/statements/drop-assembly-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
