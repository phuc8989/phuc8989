// SPDX-License-Identifier: GPL-2.0
// Copyright (C) 2017 Thomas Gleixner <tglx@linutronix.de>

#include <linux/spinlock.h>
#include <linux/seq_file.h>
#include <linux/bitmap.h>
#include <linux/percpu.h>
#include <linux/cpu.h>
#include <linux/irq.h>

#define IRQ_MATRIX_SIZE	(BITS_TO_LONGS(IRQ_MATRIX_BITS))

struct cpumap {
	unsigned int		available;
	unsigned int		allocated;
	unsigned int		managed;
	unsigned int		managed_allocated;
	bool			initialized;
	bool			online;
	unsigned long		alloc_map[IRQ_MATRIX_SIZE];
	unsigned long		managed_map[IRQ_MATRIX_SIZE];
