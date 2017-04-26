---
title: "필드 및 행 종결자 지정(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bcp utility [SQL Server], terminators
- field terminators [SQL Server]
- data formats [SQL Server], terminators
- row terminators [SQL Server]
- terminators [SQL Server]
ms.assetid: f68b6782-f386-4947-93c4-e89110800704
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 42c2ee3fe98d6c6fc35d2417469bc3eec9fddd8c
ms.lasthandoff: 04/11/2017

---
# <a name="specify-field-and-row-terminators-sql-server"></a>필드 및 행 종결자 지정(SQL Server)
  문자 데이터 필드의 경우 데이터 파일의 각 필드 끝은 *필드 종결자* 를, 그리고 각 행의 끝은 필요에 따라 *행 종결자*를 사용해 표시할 수 있습니다. 종결 문자는 프로그램이 한 개의 필드 또는 행이 끝나고 다른 필드 또는 행이 시작되는 부분을 읽도록 나타내는 한 가지 방법입니다.  
  
> [!IMPORTANT]  
>  네이티브 또는 유니코드 네이티브 형식을 사용할 때는 필드 종결자보다는 길이 접두사를 사용하십시오. 원시 형식 데이터 파일은 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 이진 데이터 형식으로 저장되므로 원시 형식 데이터와 종결자가 충돌할 수 있습니다.  
  
## <a name="characters-supported-as-terminators"></a>종결자로 지원되는 문자  
 **bcp** 명령, BULK INSERT 문 및 OPENROWSET 대량 행 집합 공급자는 다양한 문자를 필드 또는 행 종결자로 지원하며 항상 각 종결자의 첫 번째 인스턴스를 찾습니다. 다음 표에서는 종결자로 지원되는 문자를 보여 줍니다.  
  
|종결 문자|표시|  
|---------------------------|------------------|  
|탭|\t<br /><br /> 기본 필드 종결자입니다.|  
|줄 바꿈 문자|\n<br /><br /> 기본 행 종결자입니다.|  
|캐리지 리턴/줄 바꿈|\r|  
|백슬래시*|\\\|  
|Null 종결자(표시되지 않는 종결자)**|\0|  
|인쇄 가능한 모든 문자(Null, 탭, 줄 바꿈, 캐리지 리턴을 제외한 모든 제어 문자는 인쇄되지 않음)|(*, A, t, l 등)|  
|앞에서 나열된 종결 문자 중 일부 또는 전체를 포함한 최고 10개까지의 출력 가능한 문자열|(**\t\*\*, end, !!!!!!!!!!, \t—\n 등)|  
  
 *t, n, r, 0 및 '\0' 문자만 백슬래시 이스케이프 문자와 함께 사용하여 제어 문자를 생성할 수 있습니다.  
  
 **Null 제어 문자(\0)는 인쇄할 때는 표시되지 않지만 데이터 파일에서는 고유한 문자입니다. 즉, Null 제어 문자를 필드 또는 행 종결자로 사용하는 것은 필드 또는 행 종결자를 아예 사용하지 않는 것과는 다릅니다.  
  
> [!IMPORTANT]  
>  데이터 안에서 종결 문자가 나타나면 데이터가 아닌 종결자로 해석되며 종결 문자 뒤의 데이터는 다음 필드 또는 레코드에 속한 것으로 해석됩니다. 그러므로 종결자가 데이터 안에 나타나지 않도록 신중히 선택하십시오. 예를 들어 데이터에 하위 서로게이트가 포함되어 있으면 필드 종결자로 하위 서로게이트 필드 종결자는 적합하지 않습니다.  
  
## <a name="using-row-terminators"></a>행 종결자 사용  
 행 종결자가 마지막 필드의 종결자와 동일한 문자일 수 있습니다. 하지만 보통 행 종결자를 구분해 사용하는 것이 유용합니다. 예를 들어 표로 출력하려면 각 행의 마지막 필드는 줄 바꿈 문자(\n)를 사용해 종결하고 그 밖의 필드는 탭 문자(\t)를 사용해 종결합니다. 데이터 파일에 각 데이터 레코드를 별도의 줄로 배치하려면 행 종결자로 \r\n 조합을 지정하십시오.  
  
> [!NOTE]  
>  **bcp** 를 대화형으로 사용하고 \n(줄 바꿈)을 행 종결자로 지정하면 **bcp** 가 \r(캐리지 리턴) 문자를 접두사로 자동 지정하므로 \r\n이 행 종결자가 됩니다.  
  
## <a name="specifying-terminators-for-bulk-export"></a>대량 내보내기를 위한 종결자 지정  
 **char** 또는 **nchar** 데이터를 대량으로 내보내면서 기본 종결자 이외의 종결자를 사용하려는 경우 **bcp** 명령에 종결자를 지정해야 합니다. 다음 중 한 가지 방법으로 종결자를 지정할 수 있습니다.  
  
-   필드별로 종결자를 지정하는 서식 파일을 사용합니다.  
  
    > [!NOTE]  
    >  서식 파일을 사용하는 방법에 대한 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)을 참조하세요.  
  
-   서식 파일을 사용하지 않을 경우 다음과 같은 대체 방법이 있습니다.  
  
    -   **-t** 스위치를 사용하여 행의 마지막 필드를 제외한 모든 필드에 대한 필드 종결자를 지정하고 **-r** 스위치를 사용하여 행 종결자를 지정합니다.  
  
    -   필드 종결자를 탭 문자 \t로 설정하는**-t** 스위치 없이 문자 형식 스위치( **-c**또는 **-w** )를 사용합니다. 이 방식은 **-t**\t를 지정하는 것과 같습니다.  
  
        > [!NOTE]  
        >  **-n** (네이티브 데이터) 또는 **-N** (유니코드 네이티브 데이터) 스위치를 지정하면 종결자는 삽입되지 않습니다.  
  
    -   대화형 **bcp** 명령에 **in** 또는 **out** 옵션이 서식 파일 스위치(**-f**) 또는 데이터 형식 스위치(**-n**, **-c**, **-w**또는 **-N**) 없이 포함되어 있고 접두사 길이 및 필드 길이를 지정하지 않도록 선택했다면 명령에서 각 필드의 필드 종결자를 지정하라는 메시지가 표시됩니다. 기본값은 none입니다.  
  
         `Enter field terminator [none]:`  
  
         일반적으로 기본값을 사용하면 적합합니다. 하지만 **char** 또는 **nchar** 데이터 필드의 경우 다음 하위 섹션인 "종결자 사용 지침"을 참조하십시오. 컨텍스트에서 이 메시지가 표시되는 예제를 보려면 [bcp를 사용하여 데이터 형식을 호환 가능하도록 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)을 참조하세요.  
  
        > [!NOTE]  
        >  **bcp** 명령의 모든 필드를 대화형으로 지정하면 명령에서 비 XML 서식 파일의 각 필드에 대한 응답을 저장하라는 메시지를 표시합니다. 비 XML 서식 파일에 대한 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/non-xml-format-files-sql-server.md)을 참조하세요.  
  
### <a name="guidelines-for-using-terminators"></a>종결자 사용 지침  
 상황에 따라 종결자는 **char** 또는 **nchar** 데이터 필드에 유용합니다. 예를 들어  
  
-   접두사 길이 정보를 인식하지 못하는 프로그램으로 가져올 데이터 파일에서 Null 값을 포함하는 데이터 열  
  
     Null 값을 포함하는 모든 데이터 열은 가변 길이로 간주됩니다. 접두사 길이가 없는 경우 데이터가 올바르게 해석되도록 Null 필드의 끝을 식별하는 종결자가 필요합니다.  
  
-   긴 고정 길이 열. 이러한 열에 포함된 공백은 대부분의 행에서 일부만 사용합니다.  
  
     이 경우 종결자를 지정하면 저장 공간이 최소화되어 필드를 가변 길이 필드로 취급할 수 있습니다.  
  
### <a name="examples"></a>예  
 이 예에서는 `AdventureWorks.HumanResources.Department` 테이블의 데이터를 문자 형식을 사용하는 `Department-c-t.txt` 데이터 파일로 대량으로 내보내며 쉼표를 필드 종결자로, 줄 바꿈 문자(\n)를 행 종결자로 사용합니다.  
  
 **bcp** 명령에는 다음 스위치가 포함됩니다.  
  
|스위치|Description|  
|------------|-----------------|  
|**-t**|데이터 필드가 데이터 문자로 로드되도록 지정합니다.|  
|**-t** `,`|쉼표(,)를 필드 종결자로 지정합니다.|  
|**-r** \n|행 종결자를 줄 바꿈 문자로 지정합니다. 이것은 기본 행 종결자이므로 이를 지정하는 것은 선택 사항입니다.|  
|**-T**|**bcp** 유틸리티가 통합 보안을 사용하는 트러스트된 연결을 통해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 연결되도록 지정합니다. **-T** 를 지정하지 않은 경우 성공적으로 로그인하려면 **-U** 와 **-P** 를 지정해야 합니다.|  
  
 자세한 내용은 [bcp Utility](../../tools/bcp-utility.md)를 참조하세요.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 명령 프롬프트에 다음을 입력합니다.  
  
```  
bcp AdventureWorks.HumanResources.Department out C:\myDepartment-c-t.txt -c -t, -r \n -T  
```  
  
 이렇게 하면 각각 4개 필드로 된 16개의 레코드가 포함된 `Department-c-t.txt`가 생성됩니다. 필드는 열로 구분됩니다.  
  
## <a name="specifying-terminators-for-bulk-import"></a>대량 가져오기를 위한 종결자 지정  
 **char** 또는 **nchar** 데이터를 대량으로 가져올 때 대량 가져오기 명령이 데이터 파일에 사용된 종결자를 인식해야 합니다. 종결자 지정 방법은 대량 가져오기 명령에 따라 다르며 다음과 같이 지정합니다.  
  
-   **bcp**  
  
     가져오기 작업을 위해 종결자를 지정하는 구문은 내보내기 작업을 위해 종결자를 지정하는 구문과 같습니다. 자세한 내용은 이 항목의 앞부분에 나오는 "대량 내보내기를 위한 종결자 지정"을 참조하십시오.  
  
-   BULK INSERT  
  
     다음 표에서 나타나는 한정자를 사용하여 서식 파일에서 필드별로 종결자를 지정하거나 전체 데이터 파일에 대해 종결자를 지정할 수 있습니다.  
  
    |한정자|Description|  
    |---------------|-----------------|  
    |FIELDTERMINATOR **='***field_terminator***'**|문자 및 유니코드 문자 데이터 파일에 사용할 필드 종결자를 지정합니다.<br /><br /> 기본값은 \t(탭 문자)입니다.|  
    |ROWTERMINATOR **='***row_terminator***'**|문자 및 유니코드 문자 데이터 파일에 사용할 행 종결자를 지정합니다.<br /><br /> 기본값은 \n(줄 바꿈 문자)입니다.|  
  
     자세한 내용은 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)를 참조하세요.  
  
-   INSERT ... SELECT * FROM OPENROWSET(BULK...)  
  
     OPENROWSET 대량 행 집합 공급자의 경우 종결자는 서식 파일에서만 지정할 수 있습니다(큰 개체 데이터 형식 이외의 형식에 필요). 문자 데이터 파일이 기본 종결자 이외의 종결자를 사용하면 이를 서식 파일에 정의해야 합니다. 자세한 내용은 [서식 파일 만들기&#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md) 및 [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)를 참조하세요.  
  
     OPENROWSET BULK 절에 대한 자세한 내용은 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)를 참조하세요.  
  
### <a name="examples"></a>예  
 이 섹션의 예에서는 앞의 예에서 생성한 `Department-c-t.txt` 데이터 파일의 문자 데이터를 `myDepartment` 예제 데이터베이스의 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 테이블로 대량으로 가져옵니다. 예를 실행하려면 이 테이블을 만들어야 합니다. **dbo** 스키마 아래에 이 테이블을 만들려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음 코드를 실행합니다.  
  
```tsql  
USE AdventureWorks;  
GO  
DROP TABLE myDepartment;  
CREATE TABLE myDepartment   
(DepartmentID smallint,  
Name nvarchar(50),  
GroupName nvarchar(50) NULL,  
ModifiedDate datetime not NULL CONSTRAINT DF_AddressType_ModifiedDate DEFAULT (GETDATE())  
);  
GO 
```  
  
#### <a name="a-using-bcp-to-interactively-specify-terminators"></a>1. bcp를 사용하여 대화형으로 종결자 지정  
 다음 예에서는 `Department-c-t.txt` 명령을 사용하여 `bcp` 데이터 파일을 대량으로 가져옵니다. 이 명령은 대량 내보내기 명령과 동일한 명령 스위치를 사용합니다. 자세한 내용은 이 항목의 앞부분에 나오는 "대량 내보내기를 위한 종결자 지정"을 참조하십시오.  
  
 Windows 명령 프롬프트에서 다음을 입력합니다.  
  
```  
bcp AdventureWorks..myDepartment in C:\myDepartment-c-t.txt -c -t , -r \n -T  
```  
  
#### <a name="b-using-bulk-insert-to-interactively-specify-terminators"></a>2. BULK INSERT를 사용하여 대화형으로 종결자 지정  
 다음 예에서는 다음 표에 나타나는 한정자를 사용하는 `Department-c-t.txt` 문을 사용하여 `BULK INSERT` 데이터 파일을 대량으로 가져옵니다.  
  
|옵션|Attribute|  
|------------|---------------|  
|DATAFILETYPE **='**char**'**|데이터 필드가 데이터 문자로 로드되도록 지정합니다.|  
|FIELDTERMINATOR **='**`,`**'**|쉼표(`,`)를 필드 종결자로 지정합니다.|  
|ROWTERMINATOR **='**`\n`**'**|행 종결자를 줄 바꿈 문자로 지정합니다.|  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 편집기에서 다음 코드를 실행합니다.  
  
```tsql  
USE AdventureWorks;  
GO  
BULK INSERT myDepartment FROM 'C:\myDepartment-c-t.txt'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      ROWTERMINATOR = '\n'  
);  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET&#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [bcp를 사용하여 필드 길이 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)   
 [bcp를 사용하여 데이터 파일에 접두사 길이 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)   
 [bcp를 사용하여 파일 저장 유형 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
  

