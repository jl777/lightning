LIGHTNING_CLI_SRC := cli/lightning-cli.c  cli/cli_main.c cli/lightning-bet.c
LIGHTNING_CLI_OBJS := $(LIGHTNING_CLI_SRC:.c=.o)

LIGHTNING_CLI_COMMON_OBJS :=			\
	common/configdir.o			\
	common/json.o				\
	common/json_escaped.o			\
	common/version.o

BET_LIB := external/libcli.so
lightning-cli-all: cli/lightning-cli

build-bet:
	cc -shared -o $(BET_LIB)  cli/cli_main.o cli/lightning-bet.o common/configdir.o common/json.o common/json_escaped.o common/version.o ccan-asort.o ccan-autodata.o ccan-breakpoint.o ccan-crypto-hmac.o ccan-crypto-hkdf.o ccan-crypto-ripemd160.o ccan-crypto-sha256.o ccan-crypto-shachain.o ccan-crypto-siphash24.o ccan-daemonize.o ccan-err.o ccan-fdpass.o ccan-htable.o ccan-ilog.o ccan-io-io.o ccan-intmap.o ccan-io-poll.o ccan-io-fdpass.o ccan-isaac.o ccan-isaac64.o ccan-list.o ccan-mem.o ccan-noerr.o ccan-opt-helpers.o ccan-opt-parse.o ccan-opt-usage.o ccan-opt.o ccan-pipecmd.o ccan-ptr_valid.o ccan-read_write_all.o ccan-str-hex.o ccan-str.o ccan-take.o ccan-tal-grab_file.o ccan-tal-link.o ccan-tal-path.o ccan-tal-str.o ccan-tal.o ccan-time.o ccan-timer.o 
$(LIGHTNINGD_OPENING_OBJS): $(LIGHTNINGD_HEADERS) $(EXTERNAL_HEADERS)

$(LIGHTNING_CLI_OBJS) $(JSMN_OBJS): $(JSMN_HEADERS) $(COMMON_HEADERS) $(CCAN_HEADERS)

cli/lightning-cli: $(LIGHTNING_CLI_OBJS) $(LIGHTNING_CLI_COMMON_OBJS) $(JSMN_OBJS) $(CCAN_OBJS)

# Make sure these depend on everything.
ALL_PROGRAMS += cli/lightning-cli
ALL_OBJS += $(LIGHTNING_CLI_OBJS)

check-source: $(LIGHTNING_CLI_SRC:%=check-src-include-order/%)

clean: lightning-cli-clean

lightning-cli-clean:
	$(RM) $(LIGHTNING-CLI_LIB_OBJS) $(DAEMON_JSMN_OBJS)
	$(RM) $(BET_LIB)

include cli/test/Makefile
