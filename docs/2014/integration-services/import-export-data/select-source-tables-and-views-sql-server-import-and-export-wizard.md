---
title: 원본 테이블 및 뷰 선택(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 074fb9aff14a2d173658c0a8ed8e31740e957a37
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52760315"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>원본 테이블 및 뷰 선택(SQL Server 가져오기 및 내보내기 마법사)
  사용 합니다 **원본 테이블 및 뷰 선택** 페이지 테이블 및 대상에 데이터 원본에서 복사할 뷰를 지정 합니다.  
  
> [!NOTE]  
>  테이블 복사 옵션을 선택할 경우 테이블의 모든 열을 복사하지 않아도 됩니다. 대상 테이블을 선택한 후 표시할 매핑 편집을 클릭 합니다 **열 매핑** 대화 상자. 선택  **\<무시 >** 에 **대상** 열의 합니다 **열 매핑** 건너 뛰 려는 열에 대 한 대화 상자.  
  
 이 마법사에 대 한 자세한 내용은 참조 하세요 [SQL Server 가져오기 및 내보내기 마법사](import-and-export-data-with-the-sql-server-import-and-export-wizard.md)합니다. 마법사 시작 옵션에 대 한 마법사를 성공적으로 실행 하는 데 필요한 권한에 대 한 자세한 내용은 참조 하세요 [SQL Server 가져오기 및 내보내기 마법사를 실행](start-the-sql-server-import-and-export-wizard.md)합니다.  
  
 SQL Server 가져오기 및 내보내기 마법사의 목적은 원본에서 대상으로 데이터를 복사하는 것입니다. 이 마법사는 대상 데이터베이스 및 대상 테이블도 만들 수 있습니다. 그러나 여러 개의 데이터베이스 또는 테이블을 복사하거나 다른 종류의 데이터베이스 개체를 복사할 경우 대신 데이터베이스 복사 마법사를 사용해야 합니다. 자세한 내용은 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)을 참조하세요.  
  
## <a name="options"></a>변수  
  
### <a name="tables-and-views-list"></a>테이블 및 뷰 목록  
 **원본**  
 사용 가능한 목록에서 확인란을 사용하여 대상으로 복사할 테이블 및 뷰를 선택합니다. 원본 테이블 또는 뷰를 선택한 다음 다른 동작을 수행하지 않으면 원본 스키마 및 데이터가 변경되지 않고 대상으로 복사됩니다.  
  
 **대상**  
 목록에서 각 원본 테이블에 대한 대상 테이블을 선택합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]나 다른 도구를 사용하여 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 대상 테이블을 만들기 위해 마법사의 이 지점에서 일시 중지할 경우 사용 가능한 대상 테이블의 목록에 새 테이블이 즉시 표시되지는 않습니다. 단계를 대상 테이블 목록을 새로 고치려면 두 페이지를 다시 합니다 **대상 선택** 페이지에서 대상 데이터베이스를 다시 선택한 다음 다시 앞 합니다 **원본 테이블 및 뷰 선택**합니다.  
  
### <a name="other-options"></a>다른 옵션  
 **매핑 편집**  
 사용 된 **열 매핑** 대화 상자에서 원본 데이터를 받을 대상 열을 지정 합니다. 선택 하 여 열의 하위 집합만 복사할 수 있습니다 \<무시 >에 **대상** 열의 합니다 **열 매핑** 건너 뛰 려는 열에 대 한 대화 상자.  
  
 **미리 보기**  
 원본 데이터를 미리 보기는 **미리 보기 데이터** 내보내기 또는 가져오기를 수행 하기 전에 확인 대화 상자. 합니다 **미리 보기 데이터** 대화 상자에 최대 200 개의 데이터 행을 표시 합니다.  
  
 데이터를 미리 본 후 데이터 원본 및 대상에 대해 선택한 옵션을 변경할 수 있습니다. 이렇게 변경하려면 **원본 테이블 및 뷰 선택** 페이지에서 **뒤로** 를 클릭하여 선택 내용을 변경할 수 있는 이전 페이지로 돌아갑니다.  
  
  
