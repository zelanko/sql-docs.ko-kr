---
title: .dacpac 파일 추출, 게시 및 등록 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.DacTableChooser
- sql.data.tools.DacPublishDialog
- sql.data.tools.DacPropertiesDialog
- sql.data.tools.publishdacproject
- sql.data.tools.DacExtractDialog
ms.assetid: ed900f93-d3df-40f5-8e62-4d722595e041
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e77370c1afe61ff63186e7a203b9be4eeaa97849
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39088465"
---
# <a name="extract-publish-and-register-dacpac-files"></a>.dacpac 파일 추출, 게시 및 등록
이 항목에서는 SQL Server 개체 탐색기에서 연결된 데이터베이스를 마우스 오른쪽 단추로 클릭하여 수행할 수 있는 네 가지 절차에 대해 설명합니다.  
  
-   데이터 계층 응용 프로그램 게시  
  
-   데이터 계층 응용 프로그램 추출  
  
-   데이터 계층 응용 프로그램 등록  
  
-   데이터 계층 응용 프로그램 등록 취소  
  
## <a name="publish-data-tier-application"></a>데이터 계층 응용 프로그램 게시  
데이터베이스에 .dacpac를 게시할 수 있습니다. 게시 작업에서는 원본 .dacpac 파일의 스키마와 일치하도록 데이터베이스 스키마를 증분식으로 업데이트합니다. 데이터베이스가 서버에 존재하지 않을 경우 게시 작업을 통해 생성됩니다.  
  
데이터베이스 노드를 선택하여 이 작업을 사용할 수도 있습니다.  
  
.dacpac 파일을 선택합니다. .dacpac 파일을 지정하면 **DAC 속성** 단추가 사용할 수 있게 됩니다. **DAC 속성** 대화 상자에는 .dacpac 파일에 대한 정보가 표시됩니다.  
  
연결 문자열에 데이터베이스 이름이 없는 경우 데이터베이스 서버에 대한 연결 문자열을 지정하고 데이터베이스 이름을 지정합니다.  
  
이제 **게시** 및 **스크립트 생성** 단추가 사용할 수 있게 됩니다. 스크립트를 생성하면 해당 스크립트가 문서 창에서 열리므로 필요한 경우 저장할 수 있습니다. 데이터베이스에 직접 게시하도록 선택할 경우 **Data Tools 작업** 창에서 업데이트 요약과 사용되는 실제 스크립트를 볼 수 있습니다.  
  
**데이터 계층 응용 프로그램으로 등록** 확인란을 선택하면 결과 데이터베이스가 서버 메타데이터에 데이터 계층 응용 프로그램으로 등록됩니다. 게시하려는 데이터베이스가 등록된 경우 데이터베이스의 스키마가 현재 등록된 dacpac와 다르면 게시가 실패할 수 있습니다.  
  
**고급** 단추를 클릭하여 액세스할 수 있는 **고급 게시 설정** 대화 상자에서 추가 게시 구성을 사용할 수 있습니다.  
  
## <a name="extract-data-tier-application"></a>데이터 계층 응용 프로그램 추출  
데이터베이스에서 .dacpac를 추출할 수 있습니다. 추출을 수행하면 데이터베이스 스키마와 함께 사용자 테이블의 데이터가 포함되어 있을 수 있는 라이브 SQL Server 또는 Microsoft Azure SQL Database에서 데이터베이스 스냅숏 파일(.dacpac)이 만들어집니다.  
  
만들 .dacpac 파일을 지정합니다. **DAC 속성** 단추를 누르면 .dacpac 파일의 속성을 지정할 수 있는 **DAC 속성** 대화 상자가 표시됩니다.  
  
추출 프로세스의 구성을 필요한 대로 수정합니다. **추출 설정** 섹션에서는 스키마만 추출할지 스키마를 추출하고 테이블 데이터를 포함할지를 선택할 수 있습니다. 스키마와 데이터를 추출하도록 선택한 경우 데이터를 추출할 테이블을 선택할 수 있습니다.  
  
## <a name="register-data-tier-application"></a>데이터 계층 응용 프로그램 등록  
데이터베이스를 인스턴스 내에 DAC(데이터 계층 응용 프로그램)로 등록할 수 있습니다. 이렇게 하면 시스템 메타데이터의 데이터베이스 스키마에 대한 현재 상태 표현이 저장됩니다.  
  
**데이터 계층 응용 프로그램 등록** 대화 상자에서 등록된 DAC의 속성을 지정합니다.  
  
## <a name="unregister-data-tier-application"></a>데이터 계층 응용 프로그램 등록 취소  
등록 취소하면 인스턴스에서 등록된 데이터 계층 응용 프로그램의 메타데이터를 제거할 수 있습니다. 등록 취소해도 등록된 데이터베이스가 삭제되지는 않습니다.  
  
## <a name="see-also"></a>참고 항목  
[연결된 데이터베이스 개발](../ssdt/connected-database-development.md)  
  
