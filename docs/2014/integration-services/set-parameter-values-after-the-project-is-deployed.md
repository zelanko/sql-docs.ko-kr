---
title: 프로젝트를 배포한 후 매개 변수 값 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: c9dcca4d-f1a0-45ec-b078-f4d372589baf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 910de9d388e60ae3664153e2f6cb3bb5203b289c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055775"
---
# <a name="set-parameter-values-after-the-project-is-deployed"></a>프로젝트를 배포한 후 매개 변수 값 설정
  카탈로그에 프로젝트를 배포할 때 배포 마법사를 사용하여 서버 기본 매개 변수 값을 설정할 수 있습니다. 프로젝트가 카탈로그에 배포된 후 SSMS(SQL Server Management Studio) 개체 탐색기 또는 Transact-SQL을 사용하여 서버 기본값을 설정할 수 있습니다.  
  
### <a name="to-set-server-defaults-with-ssms-object-explorer"></a>SSMS 개체 탐색기를 사용하여 서버 기본값을 설정하려면  
  
1.  
  **Integration Services** 노드 아래에서 프로젝트를 선택하고 마우스 오른쪽 단추로 클릭합니다.  
  
2.  
  **속성** 을 클릭하여 **프로젝트 속성** 대화 상자를 엽니다.  
  
3.  
  **페이지 선택** 에서 **매개 변수**를 클릭하여 매개 변수 페이지를 엽니다.  
  
4.  
  **매개 변수** 목록에서 원하는 매개 변수를 선택합니다. 참고: **컨테이너** 열을 통해 패키지 매개 변수와 프로젝트 매개 변수를 구별할 수 있습니다.  
  
5.  
  **값** 열에 원하는 서버 기본 매개 변수 값을 지정합니다.  
  
 Transact-SQL로 서버 기본값을 설정하려면 [catalog.set_object_parameter_value&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database) 저장 프로시저를 사용합니다. 현재 서버 기본값을 보려면 [catalog.object_parameters&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database) 뷰를 쿼리합니다. 서버 기본값을 지우려면 [catalog.clear_object_parameter_value&#40;SSISDB 데이터베이스&#41;](/sql/integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database) 저장 프로시저를 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SSIS&#41; 매개 변수 &#40;Integration Services](integration-services-ssis-package-and-project-parameters.md)  
  
  
