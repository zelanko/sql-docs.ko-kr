---
description: ADO 보안 디자인 기능
title: ADO 보안 디자인 문제 | Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
author: rothja
ms.author: jroth
ms.openlocfilehash: fc525a10d6211ee5f15517618f2cc5b99c8abee8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88355399"
---
# <a name="ado-security-design-features"></a>ADO 보안 디자인 기능
다음 섹션에서는 ADO(ActiveX Data Objects) (ADO) 2.8 이상의 보안 디자인 기능에 대해 설명 합니다. 이러한 변경 내용은 보안을 개선 하기 위해 ADO 2.8에서 수행 되었습니다. Windows Vista의 Windows DAC 6.0에 포함 된 ADO 6.0는 Windows XP 및 Windows Server 2003의 MDAC 2.8에 포함 된 ADO 2.8와 기능적으로 동일 합니다. 이 항목에서는 ADO 2.8 이상에서 응용 프로그램의 보안을 유지 하는 방법에 대 한 정보를 제공 합니다.

> [!IMPORTANT]
>  이전 버전의 ADO에서 응용 프로그램을 업데이트 하는 경우에는 프로덕션이 아닌 컴퓨터에서 업데이트 된 응용 프로그램을 고객에 게 배포 하기 전에 테스트 하는 것이 좋습니다. 이렇게 하면 업데이트 된 응용 프로그램을 배포 하기 전에 호환성 문제를 알 수 있습니다.

## <a name="internet-explorer-file-access-scenarios"></a>Internet Explorer 파일 액세스 시나리오
 다음 기능은 Internet Explorer의 스크립팅된 웹 페이지에서 ADO 2.8 이상이 사용 되는 방식에 영향을 줍니다.

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>사용자에 게 경고 하는 데 사용 되는 수정 및 향상 된 보안 경고 메시지 상자
 ADO 2.7 이전 버전의 경우 스크립팅된 웹 페이지에서 신뢰할 수 없는 공급자의 ADO 코드를 실행 하려고 할 때 다음과 같은 경고 메시지가 나타납니다.

```console
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 ADO 2.8 이상 버전의 경우 이전 메시지가 더 이상 표시 되지 않습니다. 대신이 컨텍스트에는 다음과 같은 메시지가 나타납니다.

```console
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 앞의 메시지를 통해 사용자는 원하는 것에 대 한 결과를 알고 있을 때 의사 결정을 내릴 수 있습니다.

-   사용자가 사이트를 신뢰 하는 경우 확인을 클릭 하면 모든 디스크가 안전 하 게 보호 되는 코드 (이 항목의 뒷부분에서 설명 하는 디스크 액세스 가능 Api의 예외를 포함 하는 모든 ADO 메서드 및 속성)가 브라우저 창에서 실행 및 실행 될 수 있습니다.

-   사용자가 사이트를 신뢰 하지 않는 경우 취소를 클릭 하면 ADO 코드가 실행 중이 고 전체에서 실행 되는 데이터 액세스를 차단 합니다.

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>현재 신뢰할 수 있는 사이트로 제한 된 디스크 액세스 가능 코드
 ADO 2.8에서 특별히 제한 된 Api 집합의 기능을 제한 하 여 로컬 컴퓨터에서 파일을 읽거나 쓸 수 있는 가능성을 제공 하는 추가 디자인 변경 내용이 적용 되었습니다. Internet Explorer를 실행할 때 안전을 위해 추가로 제한 된 API 메서드는 다음과 같습니다.

-   ADO **Stream** 개체의 경우 [LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md) 또는 [SaveToFile](../../ado/reference/ado-api/savetofile-method.md) 메서드를 사용 합니다.

-   ADO **레코드 집합** 개체의 경우에는 **adcmdfile** 옵션을 설정 하거나 [Microsoft OLE DB 지 속성 공급자 (mspersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) 를 사용 하는 경우와 같이 [Save](../../ado/reference/ado-api/save-method.md) 메서드 또는 [Open](../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드 중 하나를 사용 합니다.

 이러한 제한 된 디스크 액세스 가능 함수 집합의 경우 ADO 2.8 이상에서 이러한 메서드를 사용 하는 코드가 Internet Explorer에서 실행 되는 경우 다음 동작이 발생 합니다.

-   코드를 제공한 사이트가 이전에 신뢰할 수 있는 사이트 영역 목록에 추가 된 경우이 코드는 브라우저에서 실행 되 고 로컬 파일에 액세스할 수 있는 권한이 부여 됩니다.

-   사이트가 신뢰할 수 있는 사이트 영역 목록에 표시 되지 않으면 코드가 차단 되 고 로컬 파일에 대 한 액세스가 거부 됩니다.

    > [!NOTE]
    >  ADO 2.8 이상에서 사용자는 신뢰할 수 있는 사이트 영역 목록에 사이트를 추가 하 라는 경고를 표시 하지 않습니다. 따라서 신뢰할 수 있는 사이트 목록을 관리 하는 것은 로컬 파일 시스템에 액세스 해야 하는 웹 사이트 기반 응용 프로그램을 배포 하거나 지 원하는 사용자의 책임입니다.

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>레코드 집합 개체의 ActiveCommand 속성에 대 한 액세스가 차단 되었습니다.
 Internet Explorer에서 실행 되는 경우 현재 ADO 2.8은 활성 **레코드 집합** 개체에 대 한 [ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md) 속성에 대 한 액세스를 차단 하 고 오류를 반환 합니다. 이 오류는 페이지를 신뢰할 수 있는 사이트 목록에 등록 된 웹 사이트에서 가져오는지 여부에 관계 없이 발생 합니다.

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>OLE DB 공급자 및 통합 보안에 대 한 처리의 변경 내용
 ADO 2.7 및 이전 버전에서 잠재적인 보안 문제 및 문제를 검토 하는 동안 다음과 같은 시나리오를 발견 했습니다.

 경우에 따라 통합 보안 [DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx) 속성을 지 원하는 OLE DB 공급자는 스크립팅된 웹 페이지에서 ADO 연결 개체를 다시 사용 하 여 사용자의 현재 로그인 자격 증명을 사용 하 여 실수로 다른 서버에 연결할 수 있도록 허용할 수 있습니다. 이를 방지 하기 위해 ADO 2.8 이상에서는 통합 보안에 대해 제공 하거나 제공 하지 않도록 선택한 방법에 따라 OLE DB 공급자를 처리 합니다.

 다음 표에서는 신뢰할 수 있는 사이트 영역 목록에 나열 된 사이트에서 로드 된 웹 페이지의 경우 ADO 2.8 이상에서 각 경우에 ADO 연결을 관리 하는 방법에 대 한 분석을 제공 합니다.

|사용자 인증에 대 한 IE 설정, 로그온|공급자가 "통합 보안" 및 UID 및 PWD를 지정 합니다 (SQLOLEDB).|공급자가 "통합 보안" (JOLT, MSDASQL, MSPersist)을 지원 하지 않습니다.|공급자가 "통합 보안"을 지원 하 고 SSPI로 설정 됩니다 (UID/PWD가 지정 되지 않음).|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|현재 사용자 이름 및 암호를 사용 하 여 자동 로그온|연결 허용|연결 허용|연결 허용|
|사용자 이름 및 암호 확인|연결 허용|연결 실패|연결 실패|
|인트라넷 영역 에서만 자동으로 로그온|연결 허용|사용자에 게 보안 경고 표시|사용자에 게 보안 경고 표시|
|익명 로그온|연결 허용|연결 실패|연결 실패|

 이제 보안 경고가 표시 되는 경우 메시지 상자에 사용자에 게 다음 정보가 표시 됩니다.

```console
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 앞의 메시지를 통해 사용자는 더 많은 정보를 확인 하 고 그에 따라 계속할 수 있습니다.

> [!NOTE]
>  신뢰할 수 없는 사이트의 경우 (즉, 신뢰할 수 있는 사이트 영역 목록에 나열 되지 않은 사이트) 공급자가 신뢰할 수 없는 경우 (이 섹션의 앞부분에서 설명한 대로) 사용자에 게 한 행에 두 개의 보안 경고가 표시 될 수 있습니다. 즉, 안전 하지 않은 공급자에 대 한 경고와 id 사용 시도에 대 한 두 번째 경고가 표시 될 수 있습니다. 사용자가 첫 번째 경고에 대해 확인을 클릭 하면 위의 표에 설명 된 Internet Explorer 설정 및 응답 동작 코드가 실행 됩니다.

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>암호 텍스트가 ADO 연결 문자열에 반환 되는지 여부 제어
 ADO **연결** 개체의 [ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md) 속성 값을 가져오려고 하면 다음과 같은 이벤트가 발생 합니다.

1.  연결이 열린 경우 연결 문자열을 가져오기 위해 기본 OLE DB 공급자에 초기화 호출이 수행 됩니다.

2.  [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx) 속성의 OLE DB 공급자 설정에 따라 암호는 반환 되는 다른 연결 문자열 정보와 함께 포함 됩니다.

 예를 들어 ADO 연결 동적 속성이 **보안 정보 유지** 를 **True**로 설정 하면 암호 정보가 반환 된 연결 문자열에 포함 됩니다. 그렇지 않고 기본 공급자가 속성을 **False** 로 설정 하는 경우 (예: SQLOLEDB 공급자를 사용 하는 경우) 반환 된 연결 문자열에서 암호 정보가 생략 됩니다.

 ADO 응용 프로그램 코드를 사용 하 여 타사 (타사) OLE DB 공급자를 사용 하는 경우 **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO** 속성을 구현 하는 방법을 확인 하 여 ado 연결 문자열과 함께 암호 정보가 포함 되는지 여부를 확인할 수 있습니다.

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>레코드 집합 또는 스트림을 로드 하 고 저장할 때 파일이 아닌 장치를 확인 하는 중
 ADO 2.7 및 이전 버전의 경우 파일 기반 데이터를 읽고 쓰는 데 사용 된 [Open](../../ado/reference/ado-api/open-method-ado-recordset.md) 및 [Save](../../ado/reference/ado-api/save-method.md) 와 같은 파일 입/출력 작업은 디스크 기반이 아닌 파일 형식을 지정 하는 URL 또는 파일 이름을 사용할 수 있습니다. 예를 들어 LPT1, COM2, PRN.TXT, AUX는 특정를 사용 하 여 시스템에서 프린터와 보조 장치 간의 입력/출력에 대 한 별칭으로 사용 될 수 있습니다.

 ADO 2.8 이상 버전의 경우이 기능이 업데이트 되었습니다. **레코드 집합과** **스트림** 개체를 열고 저장 하는 경우 ADO는 이제 파일 형식 검사를 수행 하 여 URL 또는 파일 이름에 지정 된 입력 또는 출력 장치가 실제 파일 인지 확인 합니다.

> [!NOTE]
>  이 섹션에서 설명 하는 파일 형식 확인은 Windows 2000 이상에만 적용 됩니다. Windows 98와 같은 이전 버전의 Windows 릴리스에서는 ADO 2.8 이상이 실행 되는 상황에는 적용 되지 않습니다.
