package coverage

import (
	"os"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW
func TestPeople_Len(t *testing.T) {
	p := People{}
	want := 10
	for i := 0; i < want; i++ {
		p = append(p, Person{})
	}
	got := len(p)
	if got != want {
		t.Errorf("Len() = %v, want %v", got, want)
	}
}

func TestPeople_Less(t *testing.T) {
	// birthDay == +firstName == + lastName == || !=

	peoples := People{
		{
			firstName: "Albert",
			lastName:  "Einstein",
			birthDay:  time.Date(1879, time.March, 14, 0, 0, 0, 0, time.UTC),
		},
		{
			firstName: "Albert",
			lastName:  "Abramovitz",
			birthDay:  time.Date(1879, time.March, 14, 0, 0, 0, 0, time.UTC),
		},
		{
			firstName: "Rudolf",
			lastName:  "Einstein",
			birthDay:  time.Date(1879, time.March, 14, 0, 0, 0, 0, time.UTC),
		},
		{
			firstName: "Hermann",
			lastName:  "Einstein",
			birthDay:  time.Date(1847, time.August, 30, 0, 0, 0, 0, time.UTC),
		},
	}

	type args struct {
		i int
		j int
	}
	tests := []struct {
		name string
		p    People
		args args
		want bool
	}{
		{
			name: "p[i].lastName >= p[j].lastName",
			p:    peoples,
			args: args{
				i: 0,
				j: 0,
			},
			want: false,
		},
		{
			name: "p[i].lastName < p[j].lastName",
			p:    peoples,
			args: args{
				i: 1,
				j: 0,
			},
			want: true,
		},
		{
			name: "p[i].firstName >= p[j].firstName",
			p:    peoples,
			args: args{
				i: 2,
				j: 0,
			},
			want: false,
		},
		{
			name: "p[i].firstName < p[j].firstName",
			p:    peoples,
			args: args{
				i: 0,
				j: 2,
			},
			want: true,
		},
		{
			name: "p[i].birthDay <= p[j].birthDay",
			p:    peoples,
			args: args{
				i: 3,
				j: 0,
			},
			want: false,
		},
		{
			name: "p[i].birthDay > p[j].birthDay",
			p:    peoples,
			args: args{
				i: 0,
				j: 3,
			},
			want: true,
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			if got := tt.p.Less(tt.args.i, tt.args.j); got != tt.want {
				t.Errorf("Less() = %v, want %v", got, tt.want)
			}
		})
	}
}

func TestPeople_Swap(t *testing.T) {
	peoples := People{
		{
			firstName: "Albert",
			lastName:  "Einstein",
			birthDay:  time.Date(1879, time.March, 14, 0, 0, 0, 0, time.UTC),
		},
		{
			firstName: "Hermann",
			lastName:  "Einstein",
			birthDay:  time.Date(1847, time.August, 30, 0, 0, 0, 0, time.UTC),
		},
	}
	type args struct {
		i int
		j int
	}
	tests := []struct {
		name string
		p    People
		args args
	}{
		{
			name: "Change the same people",
			p:    peoples,
			args: args{
				i: 0,
				j: 0,
			},
		},
		{
			name: "Change different people",
			p:    peoples,
			args: args{
				i: 0,
				j: 1,
			},
		},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			oldI := tt.p[tt.args.i]
			oldJ := tt.p[tt.args.j]
			tt.p.Swap(tt.args.i, tt.args.j)
			if oldI != tt.p[tt.args.j] {
				t.Errorf("old i (%v) != new j (%v)", oldI, tt.p[tt.args.j])
			} else if oldJ != tt.p[tt.args.i] {
				t.Errorf("old j (%v) != new i (%v)", oldJ, tt.p[tt.args.i])
			}
		})
	}
}
