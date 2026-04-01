# Python Template Base

Python 3.13+ の最小限テンプレートプロジェクト。CLI/スクリプト開発に最適化。

## 特徴

- **Python 3.13+** + [uv](https://docs.astral.sh/uv/) によるパッケージ管理
- **Ruff** (lint/format), **mypy** (型チェック strict mode), **pytest** (テスト + カバレッジ)
- **GitHub Actions** CI/CD (lint, type-check, test, security scan)
- セキュリティワークフローは [security-base](https://github.com/y-maeda1116/security-base) で一元管理

## クイックスタート

```bash
# 依存関係のインストール
uv sync --group dev

# テストの実行
uv run pytest

# リント
uv run ruff check .
uv run ruff format --check .
```

## プロジェクト構成

```
├── .github/
│   ├── workflows/
│   │   ├── ci.yml              # Ruff + mypy + pytest
│   │   ├── python-security.yml # → security-base (pip-audit + bandit)
│   │   └── secret-scan.yml     # → security-base (Trivy)
│   └── dependabot.yml
├── python_template_base/
│   └── __init__.py
├── tests/
│   ├── __init__.py
│   └── test_smoke.py
├── pyproject.toml
└── uv.lock
```

## CI/CD

| ワークフロー | 内容 | 参照先 |
|---|---|---|
| CI | Ruff, mypy, pytest | ローカル |
| Python Security | pip-audit, bandit | [security-base](https://github.com/y-maeda1116/security-base) |
| Secret Scan | Trivy | [security-base](https://github.com/y-maeda1116/security-base) |
| Dependabot | GitHub Actions 週次更新 | ローカル |

## 開発ツール

| ツール | 用途 |
|---|---|
| [uv](https://docs.astral.sh/uv/) | パッケージ管理・実行 |
| [Ruff](https://docs.astral.sh/ruff/) | Lint + Format |
| [mypy](https://mypy.readthedocs.io/) | 型チェック (strict mode) |
| [pytest](https://docs.pytest.org/) | テスト + カバレッジ |
| [pytest-cov](https://pytest-cov.readthedocs.io/) | テストカバレッジ |
| [pip-audit](https://pip-audit.readthedocs.io/) | 依存関係セキュリティスキャン |

## License

MIT
