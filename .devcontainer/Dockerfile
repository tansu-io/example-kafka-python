FROM python:3.12-slim-bookworm
COPY --from=ghcr.io/astral-sh/uv /uv /uvx /bin/
COPY --from=quay.io/minio/minio /usr/bin/mc /bin/