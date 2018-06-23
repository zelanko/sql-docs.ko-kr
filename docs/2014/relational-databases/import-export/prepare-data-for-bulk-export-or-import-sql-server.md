---
title: 대량 내보내기 또는 가져오기를 위한 데이터 준비(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- bulk importing [SQL Server], planning
- bulk importing [SQL Server], from a CSV file
- data formats [SQL Server], planning operations
- CSV files [SQL Server]
- quoted fields in CSV files [SQL Server]
ms.assetid: 783fd581-2e5f-496b-b79c-d4de1e09ea30
caps.latest.revision: 50
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6e8c73ee58adca043b3630501137285012bf3e31
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093305"
---
# <a name="prepare-data-for-bulk-export-or-import-sql-server"></a>대량 내보내기 또는 가져오기를 위한 데이터 준비(SQL Server)
  이 섹션에서는 대량 내보내기 작업을 계획하는 방법과 관련된 고려 사항 및 대량 가져오기 작업의 요구 사항에 대해 설명합니다.  
  
> [!NOTE]  
>  대량 가져오기를 위해 데이터 파일의 형식을 지정하는 방법을 확실히 모르는 경우 **bcp** 유틸리티를 사용하여 테이블에서 데이터 파일로 데이터를 내보낼 수 있습니다. 이 파일에 있는 각 데이터 필드의 서식은 데이터를 해당 테이블 열에 대량으로 가져오는 데 필요한 서식을 보여 줍니다. 데이터 파일의 필드에 대해 같은 데이터 서식을 사용합니다.  
  
## <a name="data-file-format-considerations-for-bulk-export"></a>대량 내보내기의 데이터 파일 형식 고려 사항  
 **bcp** 명령을 사용하여 대량 내보내기 작업을 수행하기 전에 다음 사항을 고려하세요.  
  
-   데이터를 파일로 내보낼 때 **bcp** 명령은 지정된 파일 이름을 사용하여 자동으로 데이터 파일을 만듭니다. 해당 파일이 이미 사용되고 있으면 데이터 파일로 대량 복사되는 데이터가 파일의 기존 내용을 덮어씁니다.  
  
-   테이블 또는 뷰에서 데이터 파일로 대량 내보내기를 수행하려면 대량 복사할 테이블 또는 뷰에 대한 SELECT 권한이 있어야 합니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 병렬 검색을 사용하여 데이터를 검색할 수 있습니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 대량으로 내보내는 테이블 행은 대개 데이터 파일에 특정 순서로 정렬되지 않을 수도 있습니다. 대량으로 내보낸 테이블 행이 데이터 파일에 특정 순서로 표시되도록 하려면 쿼리에서 대량으로 내보내는 **queryout** 옵션을 사용하고 ORDER BY 절을 지정합니다.  
  
## <a name="data-file-format-requirements-for-bulk-import"></a>대량 가져오기의 데이터 파일 형식 요구 사항  
 데이터 파일에서 데이터를 가져오려면 해당 파일은 다음과 같은 기본 요구 사항을 충족해야 합니다.  
  
-   데이터는 행 및 열 형식이어야 합니다.  
  
> [!NOTE]  
>  대량 가져오기 프로세스 동안 열을 건너뛰거나 다시 정렬할 수 있으므로 데이터 파일 구조는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 구조와 동일할 필요가 없습니다.  
  
-   데이터 파일의 데이터는 문자 또는 네이티브 형식 같이 지원되는 형식이어야 합니다.  
  
-   데이터는 문자 또는 유니코드 같은 네이티브 이진 형식일 수 있습니다.  
  
-   **bcp** 명령, BULK INSERT 문 또는 INSERT ... SELECT * FROM OPENROWSET(BULK...) 문을 사용하여 데이터를 가져오려면 대상 테이블이 이미 존재해야 합니다.  
  
-   데이터 파일의 각 필드는 대상 테이블의 해당 열과 호환 가능해야 합니다. 예를 들어 한 `int` 에 필드를 로드할 수 없습니다는 `datetime` 열입니다. 자세한 내용은 [대량 가져오기 또는 대량 내보내기를 위한 데이터 형식&#40;SQL Server&#41;](data-formats-for-bulk-import-or-bulk-export-sql-server.md) 및 [bcp를 사용하여 데이터 형식을 호환 가능하도록 지정&#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)을 참조하세요.  
  
    > [!NOTE]  
    >  전체 파일이 아니라 데이터 파일에서 가져올 행의 하위 집합을 지정하려면 **-F** *first_row* 스위치 및/또는 **-L** *last_row* 스위치와 함께 **bcp** 명령을 사용할 수 있습니다. 자세한 내용은 [bcp Utility](../../tools/bcp-utility.md)를 참조하세요.  
  
-   고정 길이 또는 고정 너비 필드가 있는 데이터 파일에서 데이터를 가져오려면 서식 파일을 사용해야 합니다. 자세한 내용은 [XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)의 두 가지 서식 파일 유형을 대량으로 내보내고 가져올 수 있습니다.  
  
-   CSV(쉼표로 구분된 값) 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대량 가져오기 작업에서 지원되지 않습니다. 그러나 경우에 따라 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 대량으로 가져오기 위한 데이터 파일로 CSV(쉼표로 구분된 값) 파일이 사용될 수 있습니다. CSV 파일의 필드 종결자로는 쉼표 이외에 다른 문자도 사용될 수 있습니다. 대량 가져오기를 위한 데이터 파일로 사용하려면 CSV 파일이 다음 제한 사항을 충족해야 합니다.  
  
    -   데이터 필드에 필드 종결자가 포함되어서는 안 됩니다.  
  
    -   모든 데이터 필드를 따옴표("")로 묶거나, 모두 묶지 않아야 합니다.  
  
     [!INCLUDE[msCoName](../../includes/msconame-md.md)] FoxPro 또는 Visual FoxPro 테이블 파일(.dbf)이나 [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 워크시트 파일(.xls)에서 대량으로 데이터를 가져오려면 앞에서 설명한 제한 사항을 준수하는 CSV 파일로 데이터를 변환해야 합니다. 일반적으로 파일 확장명은 .csv입니다. 그런 다음 .csv 파일을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 대량 가져오기 작업에서 데이터 파일로 사용할 수 있습니다.  
  
     32비트 시스템에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OPENROWSET [을 Jet용 OLE DB 공급자와 함께 사용하면 대량 가져오기 최적화를 수행하지 않아도 CSV 데이터를](/sql/t-sql/functions/openrowset-transact-sql) 테이블로 가져올 수 있습니다. Jet에서는 schema.ini 파일에 정의된 스키마를 사용하여 텍스트 파일을 테이블로 처리합니다. schema.ini 파일은 데이터 원본과 동일한 디렉터리에 있습니다.  CSV 데이터의 경우 schema.ini 파일의 매개 변수 중 하나는 "FORMAT=CSVDelimited"입니다. 이 방법을 사용하려면 Jet Test IISAMm의 작동 방식, 즉 연결 문자열 구문, schema.ini 사용법, 레지스트리 설정 옵션 등을 이해해야 합니다.  이에 대한 가장 유용한 정보는 Microsoft Access 도움말 및 KB(기술 자료) 문서에서 제공합니다. 자세한 내용은 [텍스트 데이터 원본 드라이버 초기화](http://go.microsoft.com/fwlink/?LinkId=128503), [보안된 Access 데이터베이스에 연결된 서버를 통해 SQL Server 7.0 분산 쿼리를 사용하는 방법](http://go.microsoft.com/fwlink/?LinkId=128504), [방법: Jet OLE DB 공급자 4.0을 사용하여 ISAM 데이터베이스에 연결](http://go.microsoft.com/fwlink/?LinkId=128505)및 [Jet 공급자의 텍스트 IIsam을 사용하여 구분된 텍스트 파일을 여는 방법](http://go.microsoft.com/fwlink/?LinkId=128501)을 참조하세요.  
  
 또한 데이터 파일의 데이터를 테이블로 대량으로 가져오려면 다음 요구 사항을 충족해야 합니다.  
  
-   사용자는 테이블에 대한 INSERT 및 SELECT 권한이 있어야 합니다. 사용자가 제약 조건 해제 같은 DDL(데이터 정의 언어) 작업을 필요로 하는 옵션을 사용할 경우 ALTER TABLE 권한도 있어야 합니다.  
  
-   BULK INSERT 또는 INSERT ... SELECT * FROM OPENROWSET(BULK...)를 사용하여 데이터를 대량으로 가져올 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스의 보안 프로필(사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제공 로그인을 사용하여 로그인할 경우) 또는 위임된 보안에서 사용되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 로그인으로 읽기 작업을 위해 데이터 파일에 액세스할 수 있어야 합니다. 또한 사용자는 파일을 읽을 ADMINISTER BULK OPERATIONS 권한이 있어야 합니다.  
  
> [!NOTE]  
>  분할된 뷰로 대량 가져오기는 지원되지 않고 분할된 뷰로 데이터를 대량으로 가져오려는 시도는 실패합니다.  
  
## <a name="external-resources"></a>외부 리소스  
 [Excel에서 SQL Server로 데이터를 가져오는 방법](http://support.microsoft.com/kb/321686)  
  
## <a name="change-history"></a>변경 내역  
  
|업데이트된 내용|  
|---------------------|  
|CSV 데이터를 가져오는 데 OLE DB Provider for Jet를 사용하는 방법에 대한 정보가 추가되었습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [문자 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)   
 [네이티브 형식을 사용하여 데이터 가져오기 또는 내보내기&#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
  
