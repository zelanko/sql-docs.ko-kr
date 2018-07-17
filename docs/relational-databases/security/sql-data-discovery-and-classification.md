---
title: SQL 데이터 검색 및 분류 | Microsoft Docs
description: SQL 데이터 검색 및 분류
documentationcenter: ''
ms.reviewer: carlrab
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.prod_service: sql-database,sql
ms.custom: security
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 02/13/2018
ms.author: giladm
author: giladm
manager: shaik
ms.openlocfilehash: 96861baa7fa28ef9f16f35c13f26327b824b44cc
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926334"
---
# <a name="sql-data-discovery-and-classification"></a>SQL 데이터 검색 및 분류
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

데이터 검색 및 분류는 데이터베이스에서 중요한 데이터를 **검색**, **분류**, **레이블 지정** & **보고**하는 SSMS(SQL Server Management Studio)에 기본 제공된 새로운 도구를 소개합니다.
가장 중요한 데이터(비즈니스, 재무, 보건 등)를 검색하고 분류하면 조직 정보 보호 수준에서 중요한 역할을 담당할 수 있습니다. 다음에 대한 인프라를 제공할 수 있습니다.
* 데이터 개인 정보 보호 표준을 충족하도록 지원합니다.
* 매우 중요한 데이터가 포함된 데이터베이스/열에 대한 액세스를 제어하고 보안을 강화합니다.

> [!NOTE]
> 데이터 검색 및 분류는 **SQL Server 2008 이상에 지원**됩니다. Azure SQL Database는 [Azure SQL Database 데이터 검색 및 분류](https://go.microsoft.com/fwlink/?linkid=866265)를 참조하세요.

## <a id="subheading-1"></a>개요
데이터 검색 및 분류는 고급 서비스의 집합을 소개하고 데이터베이스뿐만 아니라 데이터를 보호 대상으로 지정하는 새로운 SQL Information Protection 패러다임을 형성합니다.
* **검색 및 권장 사항** – 분류 엔진은 데이터베이스를 검사하고 잠재적으로 중요한 데이터가 포함된 열을 식별합니다. 그런 다음, 적절한 분류 권장 사항을 쉽게 검토하고 적용할 뿐만 아니라 수동으로 열을 분류하는 방법을 제공합니다.
* **레이블 지정** – 민감도 분류 레이블은 열에서 영구적으로 태그를 지정할 수 있습니다.
* **표시 유형** - 데이터베이스 분류 상태는 다른 요구 사항뿐만 아니라 규정 준수 및 감사 목적으로 사용할 인쇄/내보낼 수 있는 세부 보고서에서 볼 수 있습니다.

## <a id="subheading-2"></a>중요한 열 검색, 분류 및 레이블 지정
다음 섹션에서는 데이터베이스에서 중요한 데이터를 포함하는 열을 검색, 분류, 및 레이블을 지정할 뿐만 아니라 데이터베이스 및 내보내는 보고서의 현재 분류 상태를 보는 단계를 설명합니다.

분류에는 두 개의 메타데이터 특성이 포함됩니다.
* 레이블 - 주 분류 속성은 열에 저장된 데이터의 민감도 수준을 정의하는 데 사용합니다.  
* 정보 형식 – 열에 저장된 데이터의 형식에 대한 추가 세분성을 제공합니다.

<br>
**SQL Server 데이터베이스를 분류하려면:**

1. SSMS(SQL Server Management Studio)에서 SQL Server에 연결합니다.

2. SSMS 개체 탐색기에서 분류하려는 데이터베이스를 마우스 오른쪽 단추로 클릭하고, **작업** > **데이터 분류...** 를 선택합니다.

    ![탐색 창][1]

3. 분류 엔진은 잠재적으로 중요한 데이터를 포함하는 열에서 데이터베이스를 검사하고 **권장된 열 분류** 목록을 제공합니다.

    * 권장된 열 분류 목록을 보려면 위쪽에서 권장 사항 알림 상자 또는 창의 아래쪽에서 권장 사항 패널을 클릭합니다.

        ![탐색 창][2]

        ![탐색 창][3]

    * 권장 사항 목록을 검토합니다.
        * 특정 열에 대한 권장 사항을 허용하려면 관련 행의 왼쪽 열에서 확인란을 선택합니다. 권장 사항 테이블 헤더에서 확인란을 선택하여 *모든 권장 사항*을 수락됨으로 표시할 수도 있습니다.

        * 드롭다운 상자를 사용하여 권장되는 정보 형식 및 민감도 레이블을 변경할 수도 있습니다.        

        ![탐색 창][4]

    * 선택한 권장 사항을 적용하려면 파란색 **선택한 권장 사항 허용** 단추를 클릭합니다.

        ![탐색 창][5]

4. 대안으로 열을 **수동으로 분류**하거나 권장 사항 기반 분류로 지정할 수도 있습니다.

    * 창의 위쪽 메뉴에서 **분류 추가**를 클릭합니다.

        ![탐색 창][6]

    * 열려 있는 컨텍스트 창에서 분류하려는 스키마 > 테이블 > 열을 선택하고 정보 형식 및 민감도 레이블을 선택합니다. 컨텍스트 창의 아래쪽에 있는 파란색 **분류 추가** 단추를 클릭합니다.

        ![탐색 창][7]

5. 새 분류 메타데이터를 사용하여 분류를 완료하고 영구적으로 데이터베이스 열의 레이블(태그)을 지정하려면 창의 최상위 메뉴에서 **저장**을 클릭합니다.

    ![탐색 창][8]


6. 데이터베이스 분류 상태의 전체 요약을 사용하여 보고서를 생성하려면 창의 최상위 메뉴에서 **보고서 보기**를 클릭합니다.

    ![탐색 창][9]

    ![탐색 창][10]


## <a id="subheading-3"></a>분류 메타데이터에 액세스

*정보 유형* 및 *민감도 레이블*에 대한 분류 메타데이터는 다음 확장 속성에 저장됩니다. 
* sys_information_type_name
* sys_sensitivity_label_name

확장 속성 카탈로그 뷰[sys.extended_properties](https://docs.microsoft.com/en-us/sql/relational-databases/system-catalog-views/extended-properties-catalog-views-sys-extended-properties)를 사용하여 메타데이터에 액세스할 수 있습니다.

다음 코드 예제는 해당 분류를 사용하여 모든 분류된 열을 반환합니다.

```sql
SELECT
    schema_name(O.schema_id) AS schema_name,
    O.NAME AS table_name,
    C.NAME AS column_name,
    information_type,
    sensitivity_label 
FROM
    (
        SELECT
            IT.major_id,
            IT.minor_id,
            IT.information_type,
            L.sensitivity_label 
        FROM
        (
            SELECT
                major_id,
                minor_id,
                value AS information_type 
            FROM sys.extended_properties 
            WHERE NAME = 'sys_information_type_name'
        ) IT 
        FULL OUTER JOIN
        (
            SELECT
                major_id,
                minor_id,
                value AS sensitivity_label 
            FROM sys.extended_properties 
            WHERE NAME = 'sys_sensitivity_label_name'
        ) L 
        ON IT.major_id = L.major_id AND IT.minor_id = L.minor_id
    ) EP
    JOIN sys.objects O
    ON  EP.major_id = O.object_id 
    JOIN sys.columns C 
    ON  EP.major_id = C.object_id AND EP.minor_id = C.column_id
```

## <a id="subheading-4"></a>다음 단계

Azure SQL Database는 [Azure SQL Database 데이터 검색 및 분류](https://go.microsoft.com/fwlink/?linkid=866265)를 참조하세요.

열 수준 보안 메커니즘을 적용하여 중요한 열을 보호하는 것이 좋습니다.

* [동적 데이터 마스킹](https://docs.microsoft.com/en-us/sql/relational-databases/security/dynamic-data-masking) 사용 중인 중요한 열을 난독 처리합니다.
* [항상 암호화](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/always-encrypted-database-engine) 중요한 미사용 열을 암호화합니다.

<!--Anchors-->
[SQL Data Discovery & Classification overview]: #subheading-1
[Discovering, classifying & labeling sensitive columns]: #subheading-2
[Accessing the classification metadata]: #subheading-3
[Next Steps]: #subheading-4

<!--Image references-->
[1]: ./media/sql-data-discovery-and-classification/1_data_classification_explorer_menu.png
[2]: ./media/sql-data-discovery-and-classification/2_recommendations_notification_box.png
[3]: ./media/sql-data-discovery-and-classification/3_recommendations_panel.png
[4]: ./media/sql-data-discovery-and-classification/4_recommendations.png
[5]: ./media/sql-data-discovery-and-classification/5_accept_recommendations_button.png
[6]: ./media/sql-data-discovery-and-classification/6_add_classification_button.png
[7]: ./media/sql-data-discovery-and-classification/7_manual_classification.png
[8]: ./media/sql-data-discovery-and-classification/8_save.png
[9]: ./media/sql-data-discovery-and-classification/9_view_report.png
[10]: ./media/sql-data-discovery-and-classification/10_report.png
