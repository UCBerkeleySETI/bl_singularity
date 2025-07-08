NAME=bliss

DESTDIR=
PREFIX=/usr/local
BINDIR=$(PREFIX)/bin
BLISSPROGS=bliss_find_hits \
	   bliss_generate_channelizer_response \
	   bliss_hits_to_dat

SINGULARITY=singularity

default: sif

$(NAME).sandbox: $(NAME).def
	sudo $(SINGULARITY) build -B /usr/local/cuda --sandbox $@ $^

$(NAME).sif: $(NAME).def
	sudo $(SINGULARITY) build -B /usr/local/cuda $@ $^

sif: $(NAME).sif

sandbox: $(NAME).sandbox

install: $(NAME).sif bliss_runner
	mkdir -p "${DESTDIR}${BINDIR}"
	cp $(NAME).sif ${DESTDIR}${BINDIR}/.
	sed -e 's/-singularity/-$(SINGULARITY)/' bliss_runner > ${DESTDIR}${BINDIR}/bliss_runner
	chmod 755 ${DESTDIR}${BINDIR}/bliss_runner
	cd ${DESTDIR}${BINDIR} && for f in $(BLISSPROGS); do ln -sf bliss_runner $$f; done

clean:
	sudo rm -rf $(NAME).sif

veryclean:
	sudo rm -rf $(NAME).sif $(NAME).sandbox

.PHONY:
	sandbox sif clean veryclean
