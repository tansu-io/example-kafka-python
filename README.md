# Kafka Python with Tansu

Tansu is a Kafka compatible broker that stores data in S3 or PostgreSQL.
This example uses [kafka-python](https://github.com/dpkp/kafka-python),
with [MinIO S3](https://min.io) or [PostgreSQL](https://www.postgresql.org)
to send and receive messages with Tansu.

[MinIO](https://min.io), [PostgreSQL](https://www.postgresql.org) and Tansu
run in [Docker](https://docs.docker.com/desktop/) for easy installation and setup.

Copy `example.env` into `.env` so that you have a local working copy:

```shell
cp example.env .env
```

To use S3 with [MinIO](https://min.io), uncomment this line and comment out
other `STORAGE_ENGINE` definitions in your `.env`:

```
STORAGE_ENGINE="s3://tansu/"
```

To use [PostgreSQL](https://www.postgresql.org), uncomment this line and
comment out other `STORAGE_ENGINE` definitions in your `.env`:

```
STORAGE_ENGINE="postgres://postgres:postgres@localhost"
```

Now, start up Minio S3, PostgreSQL and Tansu:

```shell
docker compose up -d
```

Tansu's PostgreSQL schema is set up in [compose.yaml](./compose.yaml),
requiring no extra configuration. If you're using MinIO, there are 3 extra steps.

Wait for MinIO to become ready:

```shell
docker compose exec minio /usr/bin/mc ready local
```

Then, setup some default MinIO credentials:

```shell
docker compose exec minio /usr/bin/mc alias set local http://localhost:9000 minioadmin minioadmin
```

Finally, create a bucket on MinIO for Tansu:

```shell
docker compose exec minio /usr/bin/mc mb local/tansu
```

Using [uv](https://docs.astral.sh/uv/), setup a virtual Python development environment:

```shell
mkdir -p venvs
test -d venvs/dev || uv venv -p 3.12 venvs/dev
source venvs/dev/bin/activate
```

Install [kafka-python](https://github.com/dpkp/kafka-python):

```shell
uv pip install kafka-python
```

Run the example:

```shell
python example.py
```

You should see the following output:

```
ConsumerRecord(topic='my-topic', partition=0, offset=0, timestamp=1740584217091, timestamp_type=0, key=None, value=b'test', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=4, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=1, timestamp=1740584217091, timestamp_type=0, key=None, value=b'\xc2Hola, mundo!', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=13, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=2, timestamp=1740584218091, timestamp_type=0, key=None, value=b'test', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=4, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=3, timestamp=1740584218092, timestamp_type=0, key=None, value=b'\xc2Hola, mundo!', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=13, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=4, timestamp=1740584219092, timestamp_type=0, key=None, value=b'test', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=4, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=5, timestamp=1740584219092, timestamp_type=0, key=None, value=b'\xc2Hola, mundo!', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=13, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=6, timestamp=1740584220092, timestamp_type=0, key=None, value=b'test', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=4, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=7, timestamp=1740584220092, timestamp_type=0, key=None, value=b'\xc2Hola, mundo!', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=13, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=8, timestamp=1740584221092, timestamp_type=0, key=None, value=b'test', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=4, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=9, timestamp=1740584221093, timestamp_type=0, key=None, value=b'\xc2Hola, mundo!', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=13, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=10, timestamp=1740584222093, timestamp_type=0, key=None, value=b'test', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=4, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=11, timestamp=1740584222093, timestamp_type=0, key=None, value=b'\xc2Hola, mundo!', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=13, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=12, timestamp=1740584223093, timestamp_type=0, key=None, value=b'test', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=4, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=13, timestamp=1740584223093, timestamp_type=0, key=None, value=b'\xc2Hola, mundo!', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=13, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=14, timestamp=1740584224094, timestamp_type=0, key=None, value=b'test', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=4, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=15, timestamp=1740584224094, timestamp_type=0, key=None, value=b'\xc2Hola, mundo!', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=13, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=16, timestamp=1740584225094, timestamp_type=0, key=None, value=b'test', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=4, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=17, timestamp=1740584225094, timestamp_type=0, key=None, value=b'\xc2Hola, mundo!', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=13, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=18, timestamp=1740584226094, timestamp_type=0, key=None, value=b'test', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=4, serialized_header_size=-1)
ConsumerRecord(topic='my-topic', partition=0, offset=19, timestamp=1740584226095, timestamp_type=0, key=None, value=b'\xc2Hola, mundo!', headers=[], checksum=None, serialized_key_size=-1, serialized_value_size=13, serialized_header_size=-1)
```

In this example we have used the [kafka-python](https://github.com/dpkp/kafka-python)
client to send and receive messages to Tansu a Kafka compatible broker using
S3 or PostgreSQL for storage.
