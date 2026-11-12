# 직접 경로에 등록되지 않은 Page 파일

현재 소스의 `*Page.tsx` 43개가 직접 라우트에 연결되지 않는다. 하위 구성요소로 사용되는 파일도 포함하므로 모두 폐기되거나 접근 불가능한 화면이라는 뜻은 아니다.

## 모바일앱 기능: 작업 이력은 있으나 현재 메뉴·경로 제거

| 기능 | 개발 커밋 | 현재 상태 |
|---|---|---|
| 앱푸시 발송 관리 | [0d72ddbee](https://github.com/thebusinesson/smartwork/commit/0d72ddbee) | 목록·등록·수정 코드 유지, 경로 해제 |
| 모바일 이미지 배너 관리 | [f4b0e95f2](https://github.com/thebusinesson/smartwork/commit/f4b0e95f2) | 목록·등록·수정 코드 유지, 경로 해제 |
| 모바일 이미지 배너 일자별 통계 | [bfed4d1e0](https://github.com/thebusinesson/smartwork/commit/bfed4d1e0) | 코드 유지, 경로 해제 |
| 모바일 컨텐츠 배너 관리 | [1928d8c63](https://github.com/thebusinesson/smartwork/commit/1928d8c63) | 목록·등록·수정 코드 유지, 경로 해제 |

근거: [BannerRoutes.tsx의 등록 해제 설명](https://github.com/thebusinesson/smartwork/blob/dc216b3130faabcfc1dce7dbc9bd2e3b8fbecefc/frontend/src/app/routes/domains/BannerRoutes.tsx).

## 전체 직접 미등록 파일

| 파일 | 현재 코드 참조 | 본인 직접 수정 근거 |
|---|---|---|
| `frontend/src/feature/integration/hubcollab/BulkAccountManagementPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/integration/hubcollab/ProjectCompletionPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/integration/hubcollab/vendorManagement/components/RoutingBulkEditPage.tsx` | 등록 화면의 하위 파일로 참조 | [c9f016a30](https://github.com/thebusinesson/smartwork/commit/c9f016a30b5a77d190af3fc37f463130dac525bf) |
| `frontend/src/feature/integration/hubservice/AutoTransferExceptionPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/integration/hubservice/BulkIntegrationManagementPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/integration/hubservice/CertificateOidPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/integration/hubservice/HubServiceMaintenancePage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/integration/hubservice/IntegrationInquiryPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/integration/hubservice/OpenApiLogPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/integration/hubservice/RoutingExceptionPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/integration/hubservice/VendorRoutingBulkChangePage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/integration/hubvendor/HubVendorManagementPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/integration/hubvendor/IntegrationVendorManagementPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/marketing/banner/appPushNotification/AppPushNotificationManagementPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [0d72ddbee](https://github.com/thebusinesson/smartwork/commit/0d72ddbee3af966c9f0cc595b26903b3b7468f01) |
| `frontend/src/feature/marketing/banner/appPushNotification/AppPushNotificationModificationPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [0d72ddbee](https://github.com/thebusinesson/smartwork/commit/0d72ddbee3af966c9f0cc595b26903b3b7468f01) |
| `frontend/src/feature/marketing/banner/appPushNotification/AppPushNotificationRegistrationPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [0d72ddbee](https://github.com/thebusinesson/smartwork/commit/0d72ddbee3af966c9f0cc595b26903b3b7468f01) |
| `frontend/src/feature/marketing/banner/mobileContentBanner/MobileContentBannerManagementPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [1928d8c63](https://github.com/thebusinesson/smartwork/commit/1928d8c633f014f51b2c5889281e28b2ca8a8894) |
| `frontend/src/feature/marketing/banner/mobileContentBanner/MobileContentBannerModificationPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [1928d8c63](https://github.com/thebusinesson/smartwork/commit/1928d8c633f014f51b2c5889281e28b2ca8a8894) |
| `frontend/src/feature/marketing/banner/mobileContentBanner/MobileContentBannerRegistrationPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [1928d8c63](https://github.com/thebusinesson/smartwork/commit/1928d8c633f014f51b2c5889281e28b2ca8a8894) |
| `frontend/src/feature/marketing/banner/mobileImageBanner/MobileImageBannerDailyStatisticsPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [bfed4d1e0](https://github.com/thebusinesson/smartwork/commit/bfed4d1e0a1b597a2e278a1806bed55212271279) |
| `frontend/src/feature/marketing/banner/mobileImageBanner/MobileImageBannerManagementPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [f4b0e95f2](https://github.com/thebusinesson/smartwork/commit/f4b0e95f2c9b5558c81fe3e86005398e3d0eb7fc) |
| `frontend/src/feature/marketing/banner/mobileImageBanner/MobileImageBannerModificationPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [f4b0e95f2](https://github.com/thebusinesson/smartwork/commit/f4b0e95f2c9b5558c81fe3e86005398e3d0eb7fc) |
| `frontend/src/feature/marketing/banner/mobileImageBanner/MobileImageBannerRegistrationPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [f4b0e95f2](https://github.com/thebusinesson/smartwork/commit/f4b0e95f2c9b5558c81fe3e86005398e3d0eb7fc) |
| `frontend/src/feature/service/hometaxdti/CertificateStatusPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/service/hometaxdti/HometaxMonitoringPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [2b54aaff1](https://github.com/thebusinesson/smartwork/commit/2b54aaff11caa88c69e1ccadb8cdd9374d0f2386) |
| `frontend/src/feature/service/ntstransmission/TransmissionSettingsPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) |
| `frontend/src/feature/service/openscrap/IpManagementPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [4ef5c7535](https://github.com/thebusinesson/smartwork/commit/4ef5c75358022ef285e5469d732bdd645920f2b7) |
| `frontend/src/feature/service/openscrap/OpenscrapMonitoringPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/service/openscrap/VendorManagementPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/service/taxinvoice/TaxInvoiceViewerPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [b187f0dbd](https://github.com/thebusinesson/smartwork/commit/b187f0dbd08ef0747f0a0b47722d1667c9b48fa9) |
| `frontend/src/feature/status/payment/CmsAccountListPage.tsx` | 등록 화면의 하위 파일로 참조 | [e8da746f6](https://github.com/thebusinesson/smartwork/commit/e8da746f603341b11ee3c53ef0b41e82bd4d0295) |
| `frontend/src/feature/status/payment/CmsAccountResultListPage.tsx` | 등록 화면의 하위 파일로 참조 | — |
| `frontend/src/feature/status/payment/CmsWithdrawalRequestListPage.tsx` | 등록 화면의 하위 파일로 참조 | [79eb408b7](https://github.com/thebusinesson/smartwork/commit/79eb408b7a40768f9e643779cab4c9fee9da99a7) |
| `frontend/src/feature/status/payment/CmsWithdrawalResultPage.tsx` | 등록 화면의 하위 파일로 참조 | — |
| `frontend/src/feature/support/customersupport/CustomerFaqListPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [ac9452c4c](https://github.com/thebusinesson/smartwork/commit/ac9452c4c7e9baac8823e0b9f7c9db34d9934539) |
| `frontend/src/feature/support/customersupport/CustomerNoticeListPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [ac9452c4c](https://github.com/thebusinesson/smartwork/commit/ac9452c4c7e9baac8823e0b9f7c9db34d9934539) |
| `frontend/src/feature/support/customersupport/FaqDetailPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/support/customersupport/FaqWritePage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [14c27bf0e](https://github.com/thebusinesson/smartwork/commit/14c27bf0ec84d0451f7d5393066c4de7a7d4487b) |
| `frontend/src/feature/support/customersupport/NoticeDetailPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/support/customersupport/NoticeWritePage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [14c27bf0e](https://github.com/thebusinesson/smartwork/commit/14c27bf0ec84d0451f7d5393066c4de7a7d4487b) |
| `frontend/src/feature/support/customersupport/resourceShared/pages/ResourceDetailPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | — |
| `frontend/src/feature/support/customersupport/resourceShared/pages/ResourceListPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [ac9452c4c](https://github.com/thebusinesson/smartwork/commit/ac9452c4c7e9baac8823e0b9f7c9db34d9934539) |
| `frontend/src/feature/support/customersupport/resourceShared/pages/ResourceRegisterPage.tsx` | 직접 등록 없음; 기타 참조 여부 별도 확인 | [f047049eb](https://github.com/thebusinesson/smartwork/commit/f047049eb14eadcf1e725389ffba47a5879110e0) |
