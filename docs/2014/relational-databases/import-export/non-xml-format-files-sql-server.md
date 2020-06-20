---
title: 비 XML 서식 파일(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- non-XML format files
- format files [SQL Server], non-XML format files
- bulk importing [SQL Server], format files
ms.assetid: f566db3e-0a3b-4a61-9c84-49f8d42f5760
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bea7572d8281a525c8c3a3f874ff3b55071b717d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050502"
---
# <a name="non-xml-format-files-sql-server"></a>비 XML 서식 파일(SQL Server)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 *비 XML 서식 파일* 및 *XML 서식 파일*의 두 가지 서식 파일 유형을 대량으로 내보내고 가져올 수 있습니다.  
  
 **항목 내용:**  
  
-   [이점](#Benefits)  
  
-   [비 XML 서식 파일의 구조](#Structure)  
  
-   [비 XML 서식 파일의 예](#Examples)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="benefits-of-non-xml-format-files"></a><a name="Benefits"></a> 비 XML 서식 파일의 이점  
  
-   **bcp** 명령에 **format** 옵션을 지정하여 비 XML 서식 파일을 자동으로 만들 수 있습니다.  
  
-   **bcp** 명령에 기존 서식 파일을 지정할 때 명령은 서식 파일에 기록되어 있는 값을 사용하며 파일 스토리지 형식, 접두사 길이, 필드 길이 또는 필드 종결자 입력을 요구하지 않습니다.  
  
-   문자 데이터 또는 네이티브 데이터와 같은 특정 데이터 형식의 서식 파일을 만들 수 있습니다.  
  
     각 데이터 필드에 대해 대화형으로 지정된 특성을 포함하는 비 XML 서식 파일을 만들 수 있습니다. 자세한 내용은 [bcp를 사용하여 데이터 형식을 호환 가능하도록 지정&#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)을 참조하세요.  
  
> [!NOTE]  
>  XML 서식 파일은 비 XML 서식 파일에 비해 몇 가지 이점이 있습니다. 자세한 내용은 [XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)의 두 가지 서식 파일 유형을 대량으로 내보내고 가져올 수 있습니다.  
  
##  <a name="structure-of-non-xml-format-files"></a><a name="Structure"></a> 비 XML 서식 파일의 구조  
 비 XML 서식 파일은 특정 구조의 텍스트 파일입니다. 비 XML 서식 파일은 모든 테이블 열의 필드 종결자, 필드 길이, 접두사 길이 및 파일 스토리지 유형에 대한 정보를 포함합니다.  
  
 다음 그림에서는 예제 비 XML 서식 파일에 대한 서식 파일 필드를 보여 줍니다.  
  
 ![비-XML 형식 파일 필드 식별](../../database-engine/media/mydepart-fmt-ident-c.gif "비-XML 형식 파일 필드 식별")  
  
 **버전** 및 **열 개수** 필드는 한 번만 생성해야 합니다. 다음 표에서는 해당 의미에 대해 설명합니다.  
  
|서식 파일 필드|Description|  
|------------------------|-----------------|  
|버전|버전 번호는 **bcp**를 위한 것이며 [!INCLUDE[tsql](../../includes/tsql-md.md)]은 인식하지 않습니다. **bcp** 유틸리티의 버전 번호:<br /><br /> 9.0 = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> 10.0 = [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]<br /><br /> 11.0 = [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]<br /><br /> 12.0 = [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]<br /><br /> 참고: 서식 파일을 읽는 데 사용되는 **bcp** 유틸리티(Bcp.exe)의 버전은 서식 파일을 만드는 데 사용되는 버전 이상이어야 합니다. 예를 들어 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]**bcp** 는 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]**bcp**에서 생성된 버전 10.0 서식 파일을 읽을 수 있지만 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]**bcp** 는 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]**bcp**에서 생성된 버전 12.0 서식 파일을 읽을 수 없습니다.|  
|열 수|데이터 파일의 필드 개수. 이 개수는 모든 행에서 같아야 합니다.|  
  
 다른 서식 파일 필드에서는 대량으로 가져오거나 내보낸 데이터 필드에 대해 설명합니다. 각 데이터 필드를 사용하려면 서식 파일에 있는 별도의 행이 필요합니다. 모든 서식 파일 행에는 다음 표에 설명되어 있는 서식 파일 필드에 대한 값이 포함되어 있습니다.  
  
|서식 파일 필드|Description|  
|------------------------|-----------------|  
|**호스트 파일 필드 순서**|데이터 파일에서 각 필드의 위치를 나타내는 번호. 예를 들어 행의 첫 번째 필드 번호는 1입니다.|  
|**호스트 파일 데이터 형식**|데이터 파일의 특정 필드에 저장되는 데이터 형식 표시. ASCII 데이터 파일에는 SQLCHAR을, 네이티브 형식의 데이터 파일에는 기본 데이터 형식을 사용합니다. 자세한 내용은 [bcp를 사용하여 파일 스토리지 유형 지정&#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)을 참조하세요.|  
|**접두사 길이**|필드의 길이 접두사 문자 수. 유효한 접두사 길이는 0, 1, 2, 4 및 8입니다. 길이 접두사를 지정하지 않으려면 이 값을 0으로 설정합니다. 필드에 NULL 데이터 값이 있으면 길이 접두사를 지정해야 합니다. 자세한 내용은 [bcp를 사용하여 데이터 파일에 접두사 길이 지정&#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)을 참조하세요.|  
|**호스트 파일 데이터 길이**|데이터 파일의 특정 필드에 저장된 데이터 형식의 최대 길이(바이트).<br /><br /> 구분 기호로 분리된 텍스트 파일에 대한 비 XML 서식 파일을 만드는 경우 모든 데이터 필드에 대한 호스트 파일 데이터 길이를 0으로 지정할 수 있습니다. 구분 기호로 분리된 텍스트 파일에서 접두사 길이가 0이며 종결자를 가져온 경우 필드 길이 값은 무시됩니다. 이는 필드에서 사용한 스토리지 공간이 데이터와 종결자를 합한 길이와 동일하기 때문입니다.<br /><br /> 자세한 내용은 [bcp를 사용하여 필드 길이 지정&#40;SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md)을 참조하세요.|  
|**종결자**|데이터 파일의 필드를 구분하는 구분 기호. 일반적인 종결자는 쉼표(,), 탭(\t), 줄의 끝(\r\n)입니다. 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)을 참조하세요.|  
|**서버 열 순서**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에 열이 나타나는 순서. 예를 들어 데이터 파일의 4번째 필드가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블의 6번째 열에 매핑될 경우 4번째 필드의 서버 열 순서는 6입니다.<br /><br /> 테이블의 열이 데이터 파일의 데이터를 받지 못하도록 하려면 서버 열 순서 값을 0으로 설정합니다.|  
|**서버 열 이름**|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 테이블에서 복사된 열의 이름. 필드의 실제 이름을 사용할 필요는 없지만 서식 파일의 필드를 비워 두면 안 됩니다.|  
|**열 데이터 정렬**|문자 및 유니코드 데이터를 데이터 파일에 저장하는 데 사용하는 데이터 정렬.|  
  
> [!NOTE]  
>  필드와 테이블 열의 번호 또는 순서가 서로 다른 데이터 파일로부터 대량 가져오기를 수행하도록 서식 파일을 수정할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [관련 태스크](#RelatedTasks) 를 참조하세요.  
  
##  <a name="example-of-a-non-xml-format-file"></a><a name="Examples"></a> 비 XML 서식 파일의 예  
 다음 예에서는 이전에 만든`myDepartmentIdentical-f-c.fmt`라는 비 XML 서식 파일을 보여 줍니다. 이 파일에서는 `HumanResources.Department` 예제 데이터베이스의 `AdventureWorks2012` 테이블에 있는 모든 열의 문자 데이터 필드에 대해 설명합니다.  
  
 생성된 `myDepartmentIdentical-f-c.fmt`서식 파일에는 다음 정보가 포함됩니다.  
  
```  
12.0  
4  
1       SQLCHAR       0       7       "\t"     1     DepartmentID     ""  
2       SQLCHAR       0       100     "\t"     2     Name             SQL_Latin1_General_CP1_CI_AS  
3       SQLCHAR       0       100     "\t"     3     GroupName        SQL_Latin1_General_CP1_CI_AS  
4       SQLCHAR       0       24      "\r\n"   4     ModifiedDate     ""  
```  
  
> [!NOTE]  
>  예제 비 XML 서식 파일과 관련된 서식 파일 필드를 보여 주는 그림에 대한 자세한 내용은 이 항목의 앞부분에 나오는 [비 XML 서식 파일의 구조](#Structure)를 참조하세요.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [서식 파일 만들기&#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 대량 가져오기&#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [서식 파일을 사용하여 데이터 필드 건너뛰기&#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [서식 파일을 사용하여 테이블 열을 데이터 파일 필드에 매핑&#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [서식 파일 만들기&#40;SQL Server&#41;](create-a-format-file-sql-server.md)   
 [XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)   
 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)  
  
  
