---
title: "bcp를 사용하여 데이터 형식을 호환 가능하도록 지정(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bulk exporting [SQL Server], compatibility
- bulk importing [SQL Server], compatibility
- compatibility [SQL Server], data formats
- data formats [SQL Server], compatibility
- bcp utility [SQL Server], compatibility
ms.assetid: cd5fc8c8-eab1-4165-9468-384f31e53f0a
caps.latest.revision: 38
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: aecc25b2c402c27d2a425107565573ba0390effa
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="specify-data-formats-for-compatibility-when-using-bcp-sql-server"></a>bcp를 사용하여 데이터 형식을 호환 가능하도록 지정(SQL Server)
  이 항목에서는 데이터 형식 특성과 필드별 프롬프트에 대해 설명하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**bcp** 명령의 비 xml 서식 파일에 필드 단위 데이터를 저장하는 방법에 대해 설명합니다. 이러한 개념을 잘 알고 있으면 다른 데이터베이스 프로그램과 같은 다른 프로그램으로 대량으로 가져오기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 대량으로 내보낼 때 특히 유용합니다. 원본 테이블의 기본 데이터 형식(네이티브, 문자 또는 유니코드)이 다른 프로그램에서 필요한 데이터 레이아웃과 호환되지 않을 수 있습니다. 호환되지 않는 경우 데이터를 내보낼 때는 데이터 레이아웃을 지정해야 합니다.  
  
> [!NOTE]  
>  데이터를 가져오거나 내보내기 위한 데이터 형식에 익숙하지 않은 경우 [대량 가져오기 또는 대량 내보내기를 위한 데이터 형식&#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)을 참조하세요.  
  
  
##  <a name="bcpDataFormatAttr"></a> bcp 데이터 형식 특성  
 **bcp** 명령을 사용하면 데이터 파일 내 각 필드의 구조를 다음 데이터 형식 특성에 따라 지정할 수 있습니다.  
  
-   파일 저장 유형  
  
     *파일 저장 유형* 은 데이터 파일에서 데이터가 저장되는 방법을 설명합니다. 데이터는 데이터베이스 테이블 형식(네이티브 형식), 문자 표시(문자 형식) 또는 암시적 변환을 지원하는 모든 데이터 형식의 데이터 파일로 내보낼 수 있습니다. 예를 들어 **smallint** 를 **int**로 복사할 수 있습니다. 사용자 정의 데이터 형식은 해당 기본 형식으로 내보내집니다. 자세한 내용은 [bcp를 사용하여 파일 저장 유형 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)을 참조하세요.  
  
-   접두사 길이  
  
     원시 형식의 데이터를 데이터 파일에 대량으로 내보내는 작업에서 파일 저장소를 가장 적게 사용하도록 하기 위해 **bcp** 명령은 각 필드의 이름 앞에 필드 길이를 나타내는 문자를 하나 이상 추가합니다. 이러한 문자를 *길이 접두사 문자*라고 합니다. 자세한 내용은 [bcp를 사용하여 데이터 파일에 접두사 길이 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)을 참조하세요.  
  
-   필드 길이  
  
     필드 길이는 데이터를 문자 형식으로 표시하는 데 필요한 최대 문자 수를 나타냅니다. 데이터가 네이티브 형식으로 저장된 경우에는 필드 길이를 미리 알 수 있습니다. 자세한 내용은 [bcp를 사용하여 필드 길이 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)을 참조하세요.  
  
-   필드 종결자  
  
     문자 데이터 필드에서 필요에 따라 종료 문자를 사용하면 데이터 파일 내 각 필드( *필드 종결자*사용)와 행( *행 종결자*사용)의 끝을 표시할 수 있습니다. 종결 문자는 한 필드나 행이 끝나고 다른 필드나 행이 시작하는 부분을 표시하여 데이터 파일을 읽는 프로그램에 전달하는 한 방법입니다. 자세한 내용은 [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)을 참조하세요.  
  
  
##  <a name="FieldSpecificPrompts"></a> 필드별 프롬프트 개요  
 대화형 **bcp** 명령에 **in** 또는 **out** 옵션은 있으나 서식 파일 스위치(**-f**)나 데이터 형식 스위치(**-n**, **-c**, **-w**또는 **-N**)는 없는 경우 원본 또는 대상 테이블의 각 열에 대해 명령에서 각 이전 특성을 지정하라는 메시지가 차례로 표시됩니다. **bcp** 명령은 각 메시지에서 테이블 열의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식에 따라 기본값을 제공합니다. 모든 메시지에서 기본값을 그대로 사용하면 명령줄에서 네이티브 형식(**-n**)을 지정한 것과 동일한 결과가 생성됩니다. 각 프롬프트에서 기본값은 [*default*]와 같이 대괄호에 묶여 표시됩니다. 표시된 기본값을 적용하려면 Enter 키를 누릅니다. 기본값 이외의 값을 지정하려면 프롬프트에서 새 값을 입력합니다.  
  
### <a name="example"></a>예제  
 다음 예에서는 **bcp** 명령을 사용하여 대화형으로 `HumanResources.myTeam` 테이블에서 `myTeam.txt` 파일로 대량 데이터 내보내기를 수행합니다. 예를 실행하려면 이 테이블을 만들어야 합니다. 테이블 및 테이블을 만드는 방법은 [HumanResources.myTeam 예제 테이블&#40;SQL Server&#41;](../../relational-databases/import-export/humanresources-myteam-sample-table-sql-server.md)을 참조하세요.  
  
 명령에서 서식 파일이나 데이터 형식을 지정하지 않기 때문에 **bcp**는 데이터 형식 정보를 묻는 메시지를 표시합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 명령 프롬프트에 다음을 입력합니다.  
  
```  
bcp AdventureWorks.HumanResources.myTeam out myTeam.txt -T  
```  
  
 각 열에 대해 bcp는 필드별 값을 묻는 프롬프트를 표시합니다. 다음 예는 테이블의 `EmployeeID` 및 `Name` 열에 대한 필드별 프롬프트를 보여 주며 각 열에 대한 기본 파일 저장 유형(네이티브 형식)을 제안합니다. `EmployeeID` 및 `Name` 열의 접두사 길이는 각각 0, 2입니다. 사용자는 각 필드의 종결자로 쉼표(`,`)를 지정합니다.  
  
 `Enter the file storage type of field EmployeeID [smallint]:`  
  
 `Enter prefix-length of field EmployeeID [0]:`  
  
 `Enter field terminator [none]:,`  
  
 `Enter the file storage type of field Name [nvarchar]:`  
  
 `Enter prefix length of field Name [2]:`  
  
 `Enter field terminator [none]:,`  
  
 `.`  
  
 `.`  
  
 `.`  
  
 각 테이블 열에 대한 프롬프트(필요한 경우에만)가 순서대로 표시됩니다.  
  
  
##  <a name="FieldByFieldNonXmlFF"></a> 비 XML 서식 파일에 필드 단위 데이터 저장  
 테이블 열이 모두 지정된 후 **bcp** 명령은 방금 입력한 필드 단위 정보를 저장할 비 XML 서식 파일을 필요에 따라 생성할지를 묻는 메시지를 표시합니다(이전 예 참조). 서식 파일 생성하도록 선택하면 해당 테이블에서 데이터를 내보내거나 구조가 비슷한 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 가져올 때마다 서식 파일을 생성할 수 있습니다.  
  
> [!NOTE]  
>  서식 파일을 사용하면 데이터 파일에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스로 데이터를 대량 가져오거나 테이블에서 데이터를 대량 내보낼 때 서식을 다시 지정할 필요가 없습니다. 자세한 내용은 [데이터를 가져오거나 내보내기 위한 서식 파일&#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)을 참조하세요.  
  
 다음 예에서는 `myFormatFile.fmt`라는 비 XML 서식 파일을 만듭니다.  
  
 `Do you want to save this format information in a file? [Y/n] y`  
  
 `Host filename: [bcp.fmt]myFormatFile.fmt`  
  
 서식 파일의 기본 이름은 bcp.fmt지만 필요하다면 다른 이름을 지정할 수 있습니다.  
  
> [!NOTE]  
>  문자 또는 네이티브 형식과 같은 하나의 데이터 형식으로 파일을 저장하는 데이터 파일의 경우 **format** 옵션을 사용하면 데이터를 내보내거나 가져올 필요 없이 즉시 형식 파일을 만들 수 있습니다. 이 방법은 쉽고, XML 서식 파일뿐 아니라 비 XML 서식 파일도 만들 수 있다는 장점이 있습니다. 자세한 내용은 [서식 파일 만들기&#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)를 참조하세요.  
  
  
## <a name="related-tasks"></a>관련 태스크  
  
-   [bcp를 사용하여 파일 저장 유형 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
-   [bcp를 사용하여 데이터 파일에 접두사 길이 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [bcp를 사용하여 필드 길이 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)  
  
-   [필드 및 행 종결자 지정&#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
## <a name="related-content"></a>관련 내용  
 없음  
  
## <a name="see-also"></a>참고 항목  
 [데이터 대량 가져오기 및 내보내기&#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [대량 가져오기 또는 대량 내보내기를 위한 데이터 형식&#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
