# Cloud Design Patterns

## 概要
Azure アーキテクチャ センターにある[クラウド設計パターン](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/#catalog-of-patterns)の中で、一目でわかりにくいパターンについて補足する

## [アンバサダー (Ambassador)](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/ambassador)
Ambassador は、**特使、大使**といった意味の単語だが、単語の意味からはパターンが想像しにくい。アンバサダーパターンは、レガシーアプリケーションや変更が困難なアプリケーションに対して、プロキシー的に配置する事でリトライや監視などレジリエントな機能を追加するパターンである

| ![Ambassador](images/ambassador.png) |
| ----- |

- アンバサダーにオフロードされる機能は、アプリケーションとは別に管理でき、アプリケーションの従来の機能を妨げることなく、更新および変更が可能

- アンバサダーサービスは、サイドカーとしてデプロイすることができ、デーモンまたはWindowsサービスとしてもデプロイ可能

- 注意事項として、プロキシは待機時間のオーバーヘッドをもたらす可能性があり、クライアント・アプリケーションが変更出来るのであれば**クライアント側に直接実装する**方が適切な場合もある

## [破損対策レイヤー (Anti-corruption Layer)](https://learn.microsoft.com/ja-jp/azure/architecture/patterns/anti-corruption-layer)
レガシーシステムの段階的な移行や、外部システムとの相互運用が必要な場合に用いられる設計パターンです。破損対策レイヤーを設ける事で、新しいシステムが古いインフラストラクチャやプロトコルに依存せずに済みます

| ![Ambassador](images/anti-corruption-layer.png) |
| ----- |

- 独立したサービスとして実装する場合、マイクロサービスアーキテクチャを採用し、Kubernetes などのコンテナ技術を使用することが推奨されます

- 新旧システム間の統合を維持し続けることができ、移行の途中で発生する問題を最小限に抑えることができます。また、レガシシステムの機能を段階的に新しいシステムに移行する際の柔軟性も高まります