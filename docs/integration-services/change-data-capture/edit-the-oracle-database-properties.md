---
title: Oracle 데이터베이스 속성 편집 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraProp
ms.assetid: 58dc99f1-ee6b-4508-bb66-2bc589611ff7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e9178a16bf828d585e5f9fd3ae74a905fa6a0428
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298780"
---
# <a name="edit-the-oracle-database-properties"></a>Oracle 데이터베이스 속성 편집

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  속성 편집기에서 Oracle 탭을 사용하여 새 인스턴스 마법사의 CDC 데이터베이스 만들기 페이지에 제공한 설명을 변경하고 Oracle 로그 마이닝 데이터베이스 연결 정보를 변경할 수 있습니다.  
  
 다음 표에서는 **Oracle** 탭에 표시되는 정보를 설명합니다.  
  
 **이름**  
 새 인스턴스 마법사의 CDC 데이터베이스 만들기 페이지에 입력한 CDC 인스턴스의 이름입니다. 이 필드는 읽기 전용이므로 이 정보를 편집할 수 없습니다.  
  
 **설명**  
 CDC 인스턴스를 만들 때 새 인스턴스에 대한 설명을 편집하거나 추가하지 않은 경우 설명을 편집하거나 추가할 수 있습니다.  
  
 **Oracle 연결 문자열**  
 사용 중인 Oracle 데이터베이스가 있는 컴퓨터에 대한 Oracle 연결 문자열입니다. 이 필드는 읽기 전용이므로 이 정보를 편집할 수 없습니다. 연결 문자열을 변경하면 **cdc.xdbcdc_config** 테이블에 저장된 CDC 인스턴스 상태가 손상되어 Oracle CDC 인스턴스가 완전히 다른 Oracle 데이터베이스를 가리킬 수 있습니다. 약간의 변경이 필요한 경우 SQL Server Management Studio를 사용하여 구성 테이블에서 연결 문자열을 직접 변경할 수 있습니다.  
  
 **Oracle 로그 마이닝 인증**  
 로그 마이너를 포함하는 Oracle 데이터베이스에 대한 인증 자격 증명을 입력하려면 **인증**에서 다음 중 하나를 선택합니다.  
  
-   **Windows 인증**: 현재 Windows 도메인 자격 증명을 사용하려면 선택합니다. Windows 인증을 사용하도록 Oracle 데이터베이스를 구성한 경우에만 이 옵션을 사용할 수 있습니다.  
  
-   **Oracle 인증**: 이 옵션을 선택하는 경우 연결 중인 Oracle 데이터베이스의 사용자에 대한 **사용자 이름** 과 **암호** 를 입력해야 합니다.  
  
 뷰어에서 Oracle 데이터베이스 속성을 볼 수 있습니다. 뷰어를 사용할 때 정보는 읽기 전용입니다. 또한 뷰어에는 테이블에서 캡처된 열 목록이 포함되어 있습니다. 뷰어에 액세스하는 방법은 [How to Manage a CDC Instance](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [CDC Designer 콘솔에서 CDC Service를 관리하는 방법](../../integration-services/change-data-capture/how-to-manage-a-cdc-service-from-the-cdc-designer-console.md)   
 [Oracle 원본 데이터베이스에 연결](../../integration-services/change-data-capture/connect-to-an-oracle-source-database.md)   
 [Oracle에 연결](../../integration-services/change-data-capture/connect-to-oracle.md)  
  
  
