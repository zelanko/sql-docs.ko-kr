---
title: '태스크 6: 마스터 데이터 관리자를 사용 하 여 도메인 기반 특성이 생성 되었는지 확인 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6e90517a-910c-4c33-8f11-92ac3cff4fdc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: fe3f404d4f41e2977ef389216dcbc9106327266a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65488958"
---
# <a name="task-6-verify-that-the-domain-based-attribute-is-created-using-master-data-manager"></a>태스크 6: 마스터 데이터 관리자를 사용하여 도메인 기반 특성이 생성되었는지 확인
  이 작업에서는 **마스터 데이터 관리자** 를 사용해서 **State** 엔터티가 **MDS** 에 만들어졌고 **Supplier** 엔터티의 **State** 특성이 **State**엔터티에 종속된 도메인 기반 특성인지 확인합니다.  
  
1.  **마스터 데이터 관리자** 웹 애플리케이션으로 전환합니다.  
  
2.  상단에서 **SQL Server 2012 Master Data Services** 를 클릭하여 홈 페이지로 이동합니다.  
  
3.  **Suppliers** 모델이 선택되었는지 확인하고 **탐색기**를 클릭합니다. **탐색기** 가 이미 열려 있으면 페이지를 새로 고칩니다.  
  
4.  위로 마우스를 가져가서 **엔터티** 표시 되는지 확인 하 고 메뉴 모음에서 두 개의 엔터티가 있습니다. **공급 업체** 하 고 **상태**합니다.  
  
     ![상태 및 공급자가 있는 엔터티 메뉴](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-01.jpg "상태 및 공급자가 있는 엔터티 메뉴")  
  
5.  **State** 엔터티가 아직 열리지 않았으면 클릭합니다.  
  
6.  목록에서 **GA** 를 선택합니다.  
  
7.  오른쪽 **세부 정보** 창의 **오른쪽 창** 에서 **이름** 을 **Georgia**로 변경하고 **확인**을 클릭합니다.  
  
8.  다른 지역에 대해서도 위 단계를 반복합니다.  
  
    |코드|오른쪽 창|  
    |----------|----------|  
    |CA|California|  
    |CO|Colorado|  
    |IL|Illinois|  
    |DC|District of Columbia|  
    |FL|Florida|  
    |AL|Alabama|  
    |KY|Kentucky|  
    |MA|Massachusetts|  
    |AZ|Arizona|  
    |MI|Michigan|  
    |MN|Minnesota|  
    |NJ|New Jersey|  
    |NV|Nevada|  
    |NY|New York|  
    |OH|Ohio|  
    |확인|Oklahoma|  
    |또는|Oregon|  
    |PA|Pennsylvania|  
    |SC|South Carolina|  
    |KS|Kansas|  
    |TN|Tennessee|  
    |TX|Texas|  
    |UT|Utah|  
    |VA|Virginia|  
    |WA|Washington|  
    |WI|Wisconsin|  
    |HI|Hawaii|  
    |MD|Maryland|  
    |CT|Connecticut|  
  
9. State 엔터티 중 하나를 선택하고 도구 모음에서 **트랜잭션 보기** 를 클릭합니다. 방금 만든 업데이트에 대한 트랜잭션이 트랜잭션 목록에 나타납니다.  
  
10. **엔터티** 메뉴 위로 마우스를 가져가고 **Supplier**를 클릭합니다.  
  
11. 이제는 **세부 정보** 창에서 드롭 다운 목록을 사용해서 **State** 필드의 값을 변경할 수 있습니다. 또한 왼쪽 목록과 **세부 정보** 창의 드롭 다운 목록에는 코드와 이름이 중괄호로 표시됩니다. 또한 **세부 정보** 창의 다른 값도 모두 변경할 수 있습니다.  
  
     ![상태 코드 및 이름이 업데이트를 사용 하 여 특성](../../2014/tutorials/media/et-verifythatthedbaiscreatedusingmdm-02.jpg "상태 코드 및 이름이 업데이트를 사용 하 여 특성")  
  
## <a name="next-step"></a>다음 단계  
 [태스크 7: Excel에서 마스터 데이터 관리자를 사용 하 여 수행 된 업데이트 보기](../../2014/tutorials/task-7-viewing-updates-made-using-master-data-manager-in-excel.md)  
  
  
