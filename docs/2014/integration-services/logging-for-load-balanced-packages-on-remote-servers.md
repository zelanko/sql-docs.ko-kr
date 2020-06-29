---
title: 원격 서버에서 부하가 분산 된 패키지에 대 한 로깅 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], remote packages
ms.assetid: fd571567-b625-4f9a-8b7e-42c5c588b11b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b45fa6607d6edc1559d8ebcbbbc7598e11eac408
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440290"
---
# <a name="logging-for-load-balanced-packages-on-remote-servers"></a>원격 서버의 로드 균형 조정된 패키지 로깅
  모든 자식 패키지가 동일한 로그 공급자를 사용하고 동일한 대상에 쓰는 경우 관리자가 보다 쉽게 여러 서버에서 실행되는 모든 자식 패키지에 대한 로그를 관리할 수 있습니다. 모든 자식 패키지에 공통된 로그 파일을 만드는 한 가지 방법은 SQL Server 로그 공급자에 이벤트를 기록하도록 자식 패키지를 구성하는 것입니다. 모든 패키지가 동일한 데이터베이스, 동일한 서버 및 서버의 동일한 인스턴스를 사용하도록 구성할 수 있습니다.  
  
 관리자는 단일 서버에 로그온하여 모든 자식 패키지에 대한 로그 파일을 볼 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
 패키지에서 로깅을 사용하도록 설정하는 방법은 [SQL Server Data Tools에서 패키지 로깅 설정](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 로깅](performance/integration-services-ssis-logging.md)  
  
  
