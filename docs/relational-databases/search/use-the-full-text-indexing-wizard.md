---
title: 전체 텍스트 인덱싱 마법사 사용 | Microsoft Docs
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql13.swb.fulltextindexingwizard.welcome.f1
- sql13.swb.fulltextindexingwizard.selectorcreatepopschedules.f1
- sql13.swb.fulltextindexingwizard.progress.f1
- sql13.swb.fulltextindexingwizard.selectchangetracking.f1
- sql13.swb.fulltextindexingwizard.selectacatalog.f1
- sql13.swb.fulltextindexingwizard.selectatableorview.f1
- sql13.swb.fulltextindexingwizard.selectanindex.f1
- sql13.swb.fulltextindexingwizard.summary.f1
- sql13.swb.fulltextindexingwizard.selecttablecolumns.f1
helpviewer_keywords:
- Full-Text Indexing Wizard
- full-text search [SQL Server], Full-Text Indexing Wizard
ms.assetid: 3e9d9605-6525-4781-9168-fdaa06db3459
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e82b1b58fb4ed880f288ae98148f6c16da1907fd
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72903817"
---
# <a name="use-the-full-text-indexing-wizard"></a>전체 텍스트 인덱싱 마법사 사용
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SSMS에서 전체 텍스트 인덱싱 마법사는 전체 텍스트 인덱스를 만드는 과정을 단계별로 안내합니다.  
  
## <a name="create-a--full-text-index"></a>전체 텍스트 인덱스 만들기 

1. 개체 탐색기에서 전체 텍스트 인덱스를 만들 대상 테이블을 마우스 오른쪽 단추로 클릭하고 **전체 텍스트 인덱스**를 가리킨 후 **전체 텍스트 인덱스 정의**를 클릭합니다. 이 작업은 별도 창에서 마법사를 시작합니다.
   다음을 클릭합니다. 
  
2. **고유 인덱스.**  드롭다운 목록에서 인덱스를 선택합니다. 인덱스는 Null 값을 허용하지 않는 고유한 단일 키 열이어야 합니다. 전체 텍스트 고유 키에 대해 가장 작은 고유 키 인덱스를 선택합니다. 성능 향상을 위해서는 클러스터형 인덱스를 사용하는 것이 좋습니다.  
  
3.  **사용 가능한 열.** 포함할 열의 모든 열 이름 옆에 있는 상자를 선택합니다.  열 이름 옆에 있는 확인란입니다. 부적격 열은 회색으로 표시하고 해당 확인란은 비활성화됩니다.  
  
4. **단어 분리기용 언어.** 드롭다운 목록에서 언어를 선택합니다. 여기에서 선택한 언어는 인덱스에 올바른 단어 분리기를 식별하는 데 사용됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 단어 분리기를 사용하여 전체 텍스트 인덱싱된 데이터의 단어 경계를 식별합니다.  
  
5.  **유형 열.** 전체 텍스트 인덱싱되는 열의 문서 유형을 보관하는 열 이름을 선택합니다.  

> **참고:** **유형 열**은 **사용 가능한 열** 열에 이름이 지정된 열이 **varbinary(max)** 또는 **image** 유형일 경우에만 사용할 수 있습니다.  
  
6. **통계 의미 체계.** 선택한 열에 대해 의미 체계 인덱싱을 사용하도록 설정할지 여부를 선택합니다. 자세한 내용은 [의미 체계 검색&#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md)을 참조하세요.  
  
>**참고** 
>
>선택한 언어에 연결된 의미 체계 언어 모델이 없는 경우 **통계 의미 체계** 확인란은 사용하도록 설정되지 않습니다. **언어** 를 선택하기 전에 **통계 의미 체계**를 선택한 경우 드롭다운 콤보 상자에서 사용할 수 있는 언어가 의미 체계 언어 모델에서 지원하는 언어로 제한됩니다.  
>
> 의미 체계 검색은 **Azure SQL Database에서 사용할 수 없습니다.** Azure SQL Database에서 이 마법사를 실행하는 경우 통계 의미 체계 옵션이 표시되지 않습니다.
  
7. 변경 내용 추적 옵션을 선택합니다.  
  
     **자동**  
     기본 데이터가 변경될 때 자동으로 전체 텍스트 인덱스가 업데이트되도록 하려면 이 라디오 단추를 선택합니다.  
  
     **수동**  
     기본 데이터가 변경될 때 자동으로 전체 텍스트 인덱스가 업데이트되지 않도록 하려면 이 라디오 단추를 선택합니다. 기본 데이터의 변경 내용은 유지됩니다. 그러나 변경 내용을 전체 텍스트 인덱스에 적용하려면 수동으로 이 프로세스를 시작하거나 일정을 예약해야 합니다.  
  
     **변경 내용 추적 안 함**  
     기본 데이터의 변경 내용으로 전체 텍스트 인덱스가 업데이트되지 않도록 하려면 이 라디오 단추를 선택합니다.  
  
8.  인덱스가 생성될 때 전체 채우기 시작(변경 내용 추적 안 함을 선택한 경우에만 사용 가능)
  
     이 마법사가 성공적으로 완료될 때 전체 채우기를 시작하려면 이 라디오 단추를 선택합니다. 이 과정은 카탈로그에 전체 텍스트 인덱스 구조를 만드는 단계와 이 구조를 전체 텍스트 인덱싱된 데이터로 채우는 단계로 구성됩니다.  
     
     다음을 클릭합니다.
  
## <a name="catalog-index-filegroup-and-stoplist"></a>카탈로그, 인덱스 파일 그룹 및 중지 목록   
  
9.  **전체 텍스트 카탈로그 선택**  

     **카탈로그 선택:** 목록에서 전체 텍스트 카탈로그를 선택합니다. 목록에 기본 선택되어 있는 항목이 데이터베이스의 기본 카탈로그가 됩니다. 사용 가능한 카탈로그가 없으면 목록이 비활성화되고 **새 카탈로그 만들기** 확인란이 선택된 채로 비활성화됩니다.  
  
  또는
  
 10. **새 카탈로그 만들기**
 - 전체 텍스트 카탈로그를 선택합니다.  
  
    1\. **이름**  
     새 전체 텍스트 카탈로그에 사용할 이름을 입력합니다.  
  
     2\. **기본 카탈로그로 설정**  
     카탈로그를 이 데이터베이스의 기본 카탈로그로 만들려면 선택합니다.  
  
     c. **악센트 구분**  
     새 카탈로그의 악센트 구분 여부를 지정합니다. 데이터베이스에서 악센트를 구분하는 경우 **구분** 이 기본적으로 선택됩니다.  
  
     d. **인덱스 파일 그룹 선택**  
     전체 텍스트 인덱스를 만들 파일 그룹을 지정합니다.  
  
     5\. 값 선택:  
      |값|설명|  
      |-----------|-----------------|
      |**<default>**| 테이블이나 뷰가 분할되지 않은 경우 동일한 파일 그룹을 기본 테이블 또는 뷰로 사용하려면 선택합니다. 테이블 또는 뷰가 분할된 경우 기본 파일 그룹이 사용됩니다.|
      |**PRIMARY**|새 전체 텍스트 인덱스에 주 파일 그룹을 사용하려면 선택합니다.|
      *사용자가 지정한 기본 파일 그룹*|사용자 정의 기본 중지 목록이 있으면 이 목록에서 새 전체 텍스트 인덱스에 사용할 파일 그룹의 이름을 선택합니다.|   
  
     
 11. **전체 텍스트 중지 목록 선택**  
     전체 텍스트 인덱스에 사용할 중지 목록을 지정하거나 중지 목록을 사용하지 않도록 설정합니다.  
  
     중지 단어는 데이터베이스에서 중지 목록이라는 개체를 사용하여 관리됩니다. *중지 목록* 은 전체 텍스트 인덱스와 연결된 경우 해당 인덱스의 전체 텍스트 쿼리에 적용되는 중지 단어 목록입니다. 자세한 내용은 [전체 텍스트 검색에 사용할 중지 단어와 중지 목록 구성 및 관리](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)를 참조하세요.  
  
     다음 값 중 하나를 선택합니다.  
  
   |값|설명|  
    |-----------|-----------------|  
    |**<system>**|새 전체 텍스트 인덱스에 시스템 중지 목록을 사용하려면 선택합니다. 이것이 기본값입니다.|  
    |**<off>**|새 전체 텍스트 인덱스에 중지 목록을 사용하지 않으려면 선택합니다.|  
    |*user-defined-stoplist-name*|이 목록에는 데이터베이스에서 만든 각 사용자 정의 중지 목록의 이름을 표시합니다(있는 경우). 새 전체 텍스트 인덱스에 사용할 사용자 정의 중지 목록을 선택합니다.|  
  
  다음을 클릭합니다.
  
11. 필요에 따라 SQL Server만 채우기 일정을 정의합니다. 나중에 실행하도록 예약한 경우가 아니면 인덱싱 작업이 바로 시작됩니다. 예약된 시간이 되기 전까지 인덱싱 작업이 실행되지 않더라도 일정은 즉시 만들어집니다.  
  
     **새 테이블 일정**  
     테이블의 채우기 일정을 정의합니다.  
  
     **새 카탈로그 일정**  
     전체 텍스트 카탈로그의 채우기 일정을 정의합니다.  
  
     **편집**  
     일정을 편집합니다.  
  
     **Delete**  
     일정을 삭제합니다.  
  
5.  전체 텍스트 인덱싱 마법사의 진행을 보거나 제어합니다.  
  
     **중지**  
     현재 작업을 중단하고 이 세션 중에는 마법사가 이후의 전체 텍스트 작업을 수행하지 않도록 합니다.  
  
     **보고서**  
     모든 작업의 실행이 완료되면 이 단추를 클릭하여 수행된 작업에 대한 보고서에 액세스합니다. 보고서를 확인하거나 파일로 인쇄하거나 클립보드에 복사하거나 전자 메일로 보낼 수 있습니다.  
  
  
